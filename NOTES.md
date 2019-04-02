# General Notes

## Ansible

To create a new role:

```sh
molecule init role -r my-role -d docker
cd my-role/
python3 -m venv .venv
source .venv/bin/activate
pip install molecule[docker] docker-py
```

It still doesn't work after this because of missing `SELinux` stuff, a bunch
of nonsense happens and this is what worked:

```sh
cp -R /usr/lib64/python3.7/site-packages/selinux \
  .venv/lib/python3.7/site-packages/
cp -R /usr/lib64/python3.7/site-packages/_selinux.cpython-37m-x86_64-linux-gnu.so \
  .venv/lib/python3.7/site-packages/
pip uninstall docker
pip uninstall docker-py
pip install molecule[docker]
```

Do stuff ...

```sh
# things were done
molecule create
molecule converge
molecule test
```

Deactivate Python virtual environment when done working on the module.
