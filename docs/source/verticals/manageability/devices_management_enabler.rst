.. _Devices managment enabler:

#########################
Devices managment enabler
#########################

.. contents::
  :local:
  :depth: 1

***************
Introduction
***************
The main functionality of this enabler will be to register: (i) a smart IoT device in a deployment, and (ii) a cluster in an ASSIST-IoT deployment, including in the latter case 
all the necessary messages to notify it to the smart orchestrator. It will also execute all the required actions related to networking for enabling connectivity among isolated/independent clusters, 
including those that have been added via VPN/SD-WAN technology. Besides, it will allow monitoring any registered node and device in the deployment, including its status (i.e., available and used resources) 
and current instantiated enablers’ components.


***************
Features
***************
This enabler is on charge of managing the two types of devices that are used in the project:

- Kubernetes clusters: register, delete and manage the status of the clusters in synchronization with the Smart Orchestrator.
- Smart IoT devices: register, delete and manage the status of the physical IoT devices where some applications will be deployed. This feature is under development.

In future versions, K8s clusters that make use of SD-WAN or VPN connections will also be managed by the enabler.


*********************
Place in architecture
*********************
The Devices managment enabler is part of the vertical plane manageability enablers. Moreover, this enabler is a user interface that is part of the Tactile dashboard enabler.

.. figure:: ./dashboard-manageability-architecture.png
   :alt: Dashboard architecture

***************
User guide
***************
This enabler is included in the Tactile Dashboard of the project, so a logged user with the right permissions can access to it by clicking its menu entry.

+--------+----------+-------------------------------+---------------------+-----------------+
| Method | Endpoint | Description                   | Payload (if needed) | Response format |
+========+==========+===============================+=====================+=================+
| GET    | /devices | Devices view of the dashboard |                     | Web page        |
+--------+----------+-------------------------------+---------------------+-----------------+

The enabler shows a table with the registered devices (at the moment only the registered clusters in the Smart Orchestrator) 
and some information: ID, name, K8s version, server url, status and creation date.

.. figure:: ./k8sclusters.png
   :alt: Devices management user interface

To register a new K8s cluster, click on the *Add a new cluster* button and a form will appear. There are two options to register a new cluster: (i) click on the file input field
and upload a kubeconfig JSON file (a example can be found below) or (ii) fill in the form manually.

Kubeconfig JSON file example:

.. code-block:: json

  {
    "name": "cluster UPV",
    "description": "cluster UPV",
    "credentials": {
      "apiVersion": "v1",
      "clusters": [
        {
          "cluster": {
            "certificate-authority-data": "LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCk1JSUM1ekNDQWMrZ0F3SUJBZ0lCQURBTkJna3Foa2lHOXcwQkFRc0ZBREFWTVJNd0VRWURWUVFERXdwcmRXSmwKY201bGRHVnpNQjRYRFRJeU1EUXdNVEE1TURNMU5sb1hEVE15TURNeU9UQTVNRE0xTmxvd0ZURVRNQkVHQTFVRQpBeE1LYTNWaVpYSnVaWFJsY3pDQ0FTSXdEUVlKS29aSWh2Y05BUUVCQlFBRGdnRVBBRENDQVFvQ2dnRUJBTWdmCnl3Um16cnUxOTM1ZjFPVXh2aGh3V0JxbkZMbHczWW93a0hVenk0MGhva3liMWd1d3VuZHd6a05tNVVnSXpVdW0KcjNHLytSVXhxS0tYRVZSQXZiQUQ3QWVkUW5XU1ozdk5VaSttck1KUTlnYWk0THhXVGtBTTVFTzhJTHYwcEFBMQpZZ3VOZCtRQ0F3bUhFWWVUa21DY1BvS05tNUxLMHl5WVNrdW1LNER2MVNUTFQ0MEZVSzZtZUFZUjJ2S1lWS1hNCjhWc0J3R0dGNHRtMGJqUWZCMkg1d1BHWk05ZWJaMWt5S1RaZU43dU1zVFN3cGVNVFhscVpxYytOZnhkeDJNQUEKTDkwVEEwZDhDMW5wQ2RuaGNqcGpkWlpDYk1EZ21Nczc5aTNZRE03Rlpwa3RNbm9wQ09QUzdRR1U4VWNHZCtleQpuVDVkd1pIanN0QXFnZFJoTkFNQ0F3RUFBYU5DTUVBd0RnWURWUjBQQVFIL0JBUURBZ0trTUE4R0ExVWRFd0VCCi93UUZNQU1CQWY4d0hRWURWUjBPQkJZRUZDMFFUenpEWmxhckJNVHR5SDcrT3oxY2NWSTRNQTBHQ1NxR1NJYjMKRFFFQkN3VUFBNElCQVFBQ0haSm1QT3NWV3lXQjRWOFhVUXJpOHZralBGc2lMYTM5R3lFa1FybXVOVzVZT0RDQQpNRXUzNjNiT1JZcTZxM1k0OEJpQVBBSkREdkc0Zy9XbFZNRUI4OXk2aHQ2VlNsckRiWW1MclU5UTdFcEJXdTR0ClNYbitJRE0yai9CT1BhWlVYNHprZ2htT1ZSc0ZJZE9zOGpIdmx0NWhMbWZlcElqam9GNzFrdHpEdEpYKzFEMW8KMlVHTEZrUS95SGpocTkxVjdNYmd6RUE0eElZdkhQenR6ZU93amJwVklnMzNLYktYOHM3Z051M3IyRGhYMnBWNgo4WE14NnkzQ2Y3TEt2K0NGUEpseXM2QWlLVTY3Z2ZSTklDMXVUbkliK2Q5ajFFMmFJcldrS1BZNXk3dzRXYUhyCmw2ZzJnYjV0Q0RuZWNIdk43ZFo0Nm5Wc2RXUHR0VXNtbCtJagotLS0tLUVORCBDRVJUSUZJQ0FURS0tLS0tCg==",
            "server": "https://192.168.250.232:6443"
          },
          "name": "cluster UPV"
        }
      ],
      "contexts": [
        {
          "context": {
            "cluster": "cluster UPV",
            "user": "kubernetes-admin2"
          },
          "name": "cluster UPV"
        }
      ],
      "current-context": "cluster UPV",
      "kind": "Config",
      "preferences": {},
      "users": [
        {
          "name": "kubernetes-admin2",
          "user": {
            "client-certificate-data": "LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCk1JSURJVENDQWdtZ0F3SUJBZ0lJVkFoYktOYy9lYkF3RFFZSktvWklodmNOQVFFTEJRQXdGVEVUTUJFR0ExVUUKQXhNS2EzVmlaWEp1WlhSbGN6QWVGdzB5TWpBME1ERXdPVEF6TlRaYUZ3MHlNekEwTURFd09UQXpOVGhhTURReApGekFWQmdOVkJBb1REbk41YzNSbGJUcHRZWE4wWlhKek1Sa3dGd1lEVlFRREV4QnJkV0psY201bGRHVnpMV0ZrCmJXbHVNSUlCSWpBTkJna3Foa2lHOXcwQkFRRUZBQU9DQVE4QU1JSUJDZ0tDQVFFQW82YmltS3ErQVViWVdUUnkKTjY4T0pmaVdRYTVXeTJFeTQxNmw0bXcrVkdmY0N3N1BiQTBuQmcxSHVZVTJDRGFEalJxaW9mWmd5bzYwVG5UcgpDQ0Fady9XL01mQ0tvemVsWU8rYUVTam5URG9OY0JnY1F2d0hPZGVYanlOYTZzdFNFT2NhVkFsZUh3SE1xdm1GCmhIMU5kSk0vSXFVV2pJKzVpU3FFMy9Fbk9tMG4xRGpGY0R0eE1BenZSWUc0RWpzYktmY0FtOWlRQ0t5d3NkSmYKYUdvYlNXSlczaDV6YTZKL3l0T3VwTi9lWVQ0ODFNQlhEL2V5MmNaSFNyNExYaGthQnJCbjFhUHQ2VHJ4bWxUTgo1Q2l2NWtOR25NakRsbkJUWXNWTENRTmhEUVlJcy8vYzBVNUQ2aXJLOGNWWGNNbnlUNVhucXc1QmRybUp2dVNECldYTkFId0lEQVFBQm8xWXdWREFPQmdOVkhROEJBZjhFQkFNQ0JhQXdFd1lEVlIwbEJBd3dDZ1lJS3dZQkJRVUgKQXdJd0RBWURWUjBUQVFIL0JBSXdBREFmQmdOVkhTTUVHREFXZ0JRdEVFODh3MlpXcXdURTdjaCsvanM5WEhGUwpPREFOQmdrcWhraUc5dzBCQVFzRkFBT0NBUUVBZldPMUU0UDBIdm5SbzhmUHN3akxtNmVoTUhPMmp1eUhrdS82ClpVWkFjN1hjTHZMaHlqbE1JZ0JEbnF4UDFRTHhGalh3emdQa3ZpcE9YQXRFdHlIZmREc01zZURGT0Z0RlRqODEKNjlKRWdEVFQ2d2UrVkw1VWJsSEZ1YnlQMCt6dndsRUxQNFlwYnZVR3U1eWdEd045Tm9NeHFOZUlHSzZlcGxiTQp4K2Y3TjNlbU1Rd0lmYUN0dmhXNlBhbndmeVJJOGRxWVNma0JsVEFJWkVnWTNUS0E0cUdDRWorZ2JrWnV2K3pUCjd5cEtLMURrNXVjWjlvc0pZeDFZOEFTemZLWUVhZDl6dU9GdnJPL3F4bnc1RUx2T0gzbmtIUURFLzBtcjR0aVIKdFM5RHlBSjE2eFRSWHo2elN1OXUyUUFxeDJ4SU40bi9uRnRDNG1PRUdqTUV5WDJoR3c9PQotLS0tLUVORCBDRVJUSUZJQ0FURS0tLS0tCg==",
            "client-key-data": "LS0tLS1CRUdJTiBSU0EgUFJJVkFURSBLRVktLS0tLQpNSUlFcEFJQkFBS0NBUUVBbzZiaW1LcStBVWJZV1RSeU42OE9KZmlXUWE1V3kyRXk0MTZsNG13K1ZHZmNDdzdQCmJBMG5CZzFIdVlVMkNEYURqUnFpb2ZaZ3lvNjBUblRyQ0NBWncvVy9NZkNLb3plbFlPK2FFU2puVERvTmNCZ2MKUXZ3SE9kZVhqeU5hNnN0U0VPY2FWQWxlSHdITXF2bUZoSDFOZEpNL0lxVVdqSSs1aVNxRTMvRW5PbTBuMURqRgpjRHR4TUF6dlJZRzRFanNiS2ZjQW05aVFDS3l3c2RKZmFHb2JTV0pXM2g1emE2Si95dE91cE4vZVlUNDgxTUJYCkQvZXkyY1pIU3I0TFhoa2FCckJuMWFQdDZUcnhtbFRONUNpdjVrTkduTWpEbG5CVFlzVkxDUU5oRFFZSXMvL2MKMFU1RDZpcks4Y1ZYY01ueVQ1WG5xdzVCZHJtSnZ1U0RXWE5BSHdJREFRQUJBb0lCQVFDYngxQUxZdnhhMnNVMgpwT1hVZTU1TUpzVmc0RU5lZGJlckYzMXdldmtaLzROR1EyTE94L1pObkhhWjhtUHNqWGZMNlg3R0RYRTFYNEhpCjdRaU5RNEZETjdvNEgzRFl6Uzl2aHFSeGtTNGJNV2Q1UEhvcWlSMlh3ZEZUUDZSYnZBN3lhQXAzMURMejhSS1IKN2ROYXVxdndPL250VUppV1ZIbVlTQkVUMnNvc29oVmk2NzIvWWw2eXZVRmkxci8rRSs2V1I2cnRuSHNTZm5IegpOSkFPL0t2cFFmaG9oSmlPMks1YUc4U2cvZzkyZ0FQWVR3bUlDK2N5WE9WamZlYnpPYlc4bVNDd3hIdnRiMjZmClQyLzlULzVoVFpQV2M5dU9aZTB5VWExd1haU205OEc0WXhMRmFXTzdFTjh3SC9ia1ZpVThydGdzdFlFMzZuMTgKYkg0UmJTeUJBb0dCQU1iOGJZRysyekIyYytwa1NzOHlxSnh3eC9UaDk1U2NzbStHZTlieEZDRkd0RENocEpZaQpKTTI3bzlUaFdkeVk3Ui9lUjAxWmpQc2JEV2tZam1Pa2NhUFcxOEo3T2dNbm9EdlhzbjRnWkFpYkNtc0ZGRnpHCjBiYjBCamliZ2QvWk9Bd0JzUUwrRDVidGdOb0RMb0ZPWEZJQzVkbmdEUFdlRU00bWVMUnZBTTE5QW9HQkFOS0sKdFFEd1YyV2FqdVFNNk1QalhVS2F3aTRiOFBlTlc3eitSUjdPM3dhRzI3V0dPTnZVRnZQV1NTSlVPT3c2WGQrOApTY0c0OUlsbHpmcGNsbTY2eElMbURTN3VjM055czkrR0d2NWN3RVdud0NoVWdVL0JmejZqcTlYUk1lZ2luZlNlCnVPaC9hbDNKQ2JHaU80c1I1UVMrbGx5WnhXekFZaURnaWNWV211YkxBb0dBS2RJMytjTHhNbmhTMkhxSHRwQ0IKRzVBZ2xuay9uYjVwU2tOTGw5dEhUYzhjWS9RMU1WQ3Z4NFdlWTBtUnAybUV2T1BzdkhjTHlHTGhLS3Qra2JhbwpJN1V0MTdRcWR5dEc1QXpyZU5LNTg0MFNYWGZOMWNuN25hWWdBSm0rYkJ1dFNlaTVHVlhvVk9KSjZJZ3VxQUtlCktLWnZSS0Z3VjljRzFTMEV4WGRuQmNrQ2dZRUF6ZEhCUG9pMXQyTFBtMHF2Wllmb0RJdURsbFhFVEF5SmlRazkKQXZBVEFLdG5MMTVtU1NoZHc4TlF2VmwrU0JpSzJvU1R5ZWlJVGFVVEpsUEt6N2FQRXJQWVlXL0R0ekdEZTlqNgpuSHlKamM1K3dDNVVOMmFlZ05xNXlnMTJiMHNnQlJvQkEzQkR5Q2tXNityL3NHVXU4R05zVkZ3U3JzeW5ZU0tBCkxFVU1xdDhDZ1lBVVpGTEF2dTNvVGZlYkpFSEw4ZCtWME1wQ3F2b1FvaVRzT3lYbG9BOFRvOTI4Z2ppQ1hFZ0cKSFdRaDlrM0J4U3pGbm5tZTZjdzJKQXZYb3lha1ZMT0FhNUtrOTVVMTVHZi8xY1Q2ZFFHWVdFMlNMWXNQVnUyQwpYNkhzckJHM244K3dYQjNHemloSjYwV3ZaSnpoZlJ2MTVHZno3cUdNUUkzVllKVEliNk1uMnc9PQotLS0tLUVORCBSU0EgUFJJVkFURSBLRVktLS0tLQo="
          }
        }
      ]
    },
    "k8s_version": "1.23"
  }



.. figure:: ./k8scluster_form.png
   :alt: Register a new K8s cluster

To delete a registered cluster, click on the *Delete cluster* button of the selected cluster and confirm the action in the dialog.

.. figure:: ./k8scluster_delete.png
   :alt: Delete a registered K8s cluster

***************
Prerequisites
***************
The Smart Orchestrator must be previously installed.

***************
Installation
***************
This enabler is part of the Tactile dashboard enabler, so see the installation section of the Tactile dashboard enabler entry.

*********************
Configuration options
*********************
TBD

***************
Developer guide
***************
For more information, read the `PUI9 wiki <https://gitlab.assist-iot.eu/wp4/applications/dashboard-pui9/-/wikis/home>`_ at Gitlab
or read the `Tactile dashboard enabler entry <https://assist-iot-enablers-documentation.readthedocs.io/en/latest/horizontal_planes/application/tactile_dashboard_enabler.html>`_

***************************
Version control and release
***************************
Version 0.1. Under development.

***************
License
***************
TBD

********************
Notice(dependencies)
********************
TBD