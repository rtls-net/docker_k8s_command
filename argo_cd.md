### argo CD 
### Installing ArgoCD on minikube
## We will start with launching minikube. There are several driver options that you can use to start a minikube cluster (virtualbox, docker, hyperv). I used docker as driver.
  `minikube start --driver=docker`

  ## Just like other Kubernetes tools, ArgoCD requires a namespace with its name. Therefore, we will create a namespace for argocd.
  `kubectl create ns argocd`


  ### We will apply ArgoCD manifest installation file from ArgoCD github repository

`kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/v2.5.8/manifests/install.yaml`

### Let’s verify the installation by getting all the objects in the ArgoCD namespace.

`kubectl get all -n argocd`

### In order to access the web GUI of ArgoCD, we need to do a port forwarding. For that we will use the argocd-server service (But make sure that pods are in a running state before running this command).
`kubectl port-forward svc/argocd-server -n argocd 8080:443`

## Now we can go to a browser and open localhost:8080

To use ArgoCD interface, we need to enter our credentials. The default username is admin so we can enter it immediately, but we will need to get the initial password from ArgoCD through minikube terminal.

Initial password is kept as a secret in the argocd namespace; therefore, we will use jsonpath query to retrieve the secret from the argocd namespace. We also need to decode it with base64. To do the both operations, just open a new terminal and enter the following code to do the trick for you. (Do not close the first terminal window as the port-forwarding is still alive)

kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo
4. Copy the password, go back to your browser and enter it as password (username is admin). You should be in the GUI interface.


Deploying a test app
Now that we are in the user interface, we can create a new app. The source code for my application is in my Github repo, so I will connect my Github repo to ArgoCD. (We could also hit new app and add our repo there, but I opted for this option first)

Click on the gear icon to open settings

2. Click on repositories


3. Click on connect repo


4. For connection method, choose HTTPS, for Project choose default, and enter your github repo as repository URL. Finally, hit on connect.


5. You should get a Successful message in terms of connection status.

6. Let’s create a new app from the repo. At the far right of the Successful message, click on the three dots. The pop up menu will have a create applicationoption. Also click that option.


7. Enter test as application name, choose default for Project Name, and choose Automatic for Sync Policy.


8. Enter repository URL (You do not have to type it down, it is already there) Enter nginx as path (My resource files are in nginx directory of my repo). Choose kubernetes.default.svc as cluster URL. Enter test as namespace (I already have a namespace object with test). Hit on Create on the top


There we go! We have our app!

9. Click anywhere on the app to get a detailed view of the application.


Desired Manifest vs Live Manifest
In the context of Argo CD, the desired manifest is the desired state of the application as defined in the version control repository (e.g. Git). The live manifest is the current state of the application as deployed in the target environment (e.g. cluster).

Argo CD continuously compares the desired manifest with the live manifest and if there are any differences, it will automatically sync the live manifest to match the desired state. This ensures that the desired state of the application is always up-to-date and consistent across all environments.

To see desired and live manifest, we just need to click on an object. If you follow along, just click on the nginx-deployment.


At the bottom of the page, you will see desired and live manifest options. Just click of them to see the state.


Also note that there is a diff option in the middle. It shows the differences in the desired manifest and live manifest if any.

Changing the live manifest
Normally, we should make the changes through GIT so that we always have our desired manifest as the live manifest. Let’s say that we made a mistake and manually changed our deployment with kubectl on our terminal.
kubectl scale deployment -n test nginx-deployment --replicas=2

As you can see, the second pod immediately appeared on the ArgoCd interface.

2. Now let’s click on the nginx-deployment again to see the diff option.


It shows that the replicasets are different. There are several methods to correct the issue. I want to point out the self-heal option.

3. Click on APP details


4. Scroll down until you see the self-heal option. Click on enable to enable self-heal process.


5. You will be asked to confirm

Are you sure you want to enable automated self healing? OK

6. As soon as we enable self-healing, the deployment scales down to 1 replica to confirm to the desired manifest.


We can also go to the nginx-deployment and check the events and logs to see how our application changed and healed.


`https://medium.com/@mehmetodabashi/installing-argocd-on-minikube-and-deploying-a-test-application-caa68ec55fbf`
