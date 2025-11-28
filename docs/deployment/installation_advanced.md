## Further Instructions for Advanced Users

### Manage your deployments using Kubeflow
To further view and manage your Katib experiments, you can use the Kubeflow Dashboard. The dashboard provides a user-friendly interface to monitor the status of your deployments and access various Kubeflow components. As platform administrator you can start the daskboard by running the following command:

```
kubectl port-forward svc/istio-ingressgateway -n istio-system 8080:80
```
Then, open your web browser and navigate to `http://localhost:8080/`. From there, you can access the Kubeflow Dashboard and explore the different components, including Katib.

<p align="center">
  <img src="/assets/platform_ui/kubeflow_cp.png" alt="CVAT" width="800">
</p>

### Monitor current running pods for debugging
To monitor the current running pods in your Kubernetes cluster, you can use the following command:

```
kubectl get pods -n name-of-the-namespace
```

There you will see a list of all the pods running in the specified namespace, along with their status, age, and other relevant information. This command is useful for debugging purposes, as it allows you to check the status of your deployments and identify any issues that may arise.

### YAML file structure for experiments
 
Each experiment in Katib is defined using a YAML file that specifies the configuration and parameters for the experiment. Below is an example of a YAML file structure for a simple experiment that uses the Random Search algorithm to optimize hyperparameters for a segmentation task:

```yaml
apiVersion: kubeflow.org/v1beta1
kind: Experiment
metadata:
  name: random-experiment
  namespace: kubeflow-user-example-com  # Ensure this matches your Kubeflow namespace
  annotations:
    katib.kubeflow.org/metrics-collector-injection: enabled  # Enable metrics collection
spec:
  objective:
    type: maximize
    goal: 0.4
    objectiveMetricName: meaniou # choose the metric to optimize
  algorithm:
    algorithmName: random
  parallelTrialCount: 1
  maxTrialCount: 1
  maxFailedTrialCount: 1
  parameters: # define hyperparameters to optimize
    - name: learning-rate
      parameterType: double
      feasibleSpace:
        min: "0.01"
        max: "0.1"
    - name: batch-size
      parameterType: int
      feasibleSpace:
        min: "2"
        max: "3"
    - name: epochs
      parameterType: int
      feasibleSpace:
        min: "1"
        max: "2"
  trialTemplate:
    primaryContainerName: training-container
    trialParameters:
      - name: learningRate
        description: Learning rate for the training job
        reference: learning-rate
      - name: batchSize
        description: Batch size for the training job
        reference: batch-size
      - name: numEpochs
        description: Number of training epochs
        reference: epochs
    trialSpec:
      apiVersion: batch/v1
      kind: Job
      spec:
        template:
          metadata:
            annotations:
              sidecar.istio.io/inject: "false"
          spec:
            containers:
              - name: training-container
                image: segmentation-utils:v1
                imagePullPolicy: IfNotPresent
                command: # define the command to run the training script
                  - "python"
                  - "-u"
                  - "/segmentation/train.py"
                  - "--config"
                  - "/segmentation/config.json"
                  - "--lr"
                  - "${trialParameters.learningRate}"
                  - "--bs"
                  - "${trialParameters.batchSize}"
                  - "--epochs"
                  - "${trialParameters.numEpochs}"
                  - --localpath
                  - add_the_timestamp
                  - --dataset 
                  - /segmentation/dataset_path
                volumeMounts:
                  - mountPath: /dev/shm
                    name: shm
                  - mountPath: /segmentation
                    name: segmentation
            volumes: #define volumes to be mounted in the container
              - name: shm
                emptyDir:
                  medium: Memory
                  sizeLimit: 32Gi
              - name: segmentation
                hostPath:
                  path: /host/Segmentation
                  type: Directory
            restartPolicy: OnFailure
``` 

A custom version of this script is applied every time the Start Training button is pressed in the platform UI. You can find the relevant code used for this implementation inside the `/Frontend/AmalthAI_WebApp/utils/experiment_organize.py` file.

### CVAT Integration

Make sure that CVAT is properly setted up and running inside your system and the right port is already updated on the main `app.py` file of the platform.