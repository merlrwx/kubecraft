- Used `clab inspect` to view running state.
- Used docker start to restart the container
- Checked inside container with docker exec, then `show interfaces brief`, it was still down.
- So redployed the lab with `clab redeploy -t topology/lab.clab.yml`
- exec back in and show interfaces. Was now connected to srl1 namespace.

