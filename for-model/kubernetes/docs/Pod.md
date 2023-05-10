
forEach: k8s.Pod
fileName: {{object.metadata.name}}.md
path: kubernetes/docs/{{object.kind}}
---

#### Object: {{object.metadata.name}}
#### Type: {{object.kind}}

### Cluster에 {{object.metadata.name}} {{object.kind}}를 생성하려면 아래의 명령어를 실행하세요.

```
kubectl create -f {{{yamlPath}}}
```
- Yaml 파일에 명시된 스펙으로 {{object.metadata.name}} {{object.kind}}를 생성합니다.

```
kubectl apply -f {{{yamlPath}}}
```
- Create가 된 상태라면 {{object.metadata.name}} {{object.kind}}의 수정이 이루어지고, Create가 된 상태가 아니라면 {{object.metadata.name}} {{object.kind}}를 Create 해주는 명령어입니다.  
#

{{include}}

### Kubernetes Cluster network 외부에서 service에 access할 때, 해당 명령어로 외부 IP traffic을 허용할 수 있습니다.

```
kubectl port-forward {{object.kind}}/{{object.metadata.name}} 8080:{{portNumber object}}
```
#

### {{object.metadata.name}} {{object.kind}}의 로그 기록을 확인하려면 아래의 명령어를 실행하세요.

```
# logs of deployment
kubectl logs {{object.kind}}/{{object.metadata.name}}

# follow logs
kubectl logs -f {{object.kind}}/{{object.metadata.name}}
```
- {{object.metadata.name}} {{object.kind}}의 로그 기록을 통해 이슈를 확인할 수 있습니다. 
#

### {{object.metadata.name}} {{object.kind}}를 삭제하려면 아래의 명령어를 실행하세요.

```
kubectl delete {{object.kind}} {{object.metadata.name}}
```
#


<function>
  window.$HandleBars.registerHelper('portNumber', function (object) {
      var port = ''

      if(object.kind=='Service'){
          port = object.spec.ports[0].port
      }else if(object.kind=='Deployment'){
          port = object.spec.template.spec.containers[0].ports[0].containerPort
      }else if(object.kind=='Pod'){
          port = object.spec.containers[0].ports[0].containerPort
      }

      return port;
  })
</function>
