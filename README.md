# dockerfiles

## Run plugin Unit Tests:
```bash
docker run -v $PWD/cloudify-terraform-plugin:/project python-3.6.5
```
## Run the requirements compilation:
```bash
docker run -v $PWD/cloudify-terraform-plugin:/project py3.6-requirements:latest
docker run -v $PWD/cloudify-terraform-plugin:/project py3.11.1-requirements:latest
```
