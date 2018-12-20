---
title: Python Virtual Environments
category: "cheat sheets"
cover: python_thumbnail.jpg
---


Why you would choose venv over mkvirtualenv:
- venv allows for matplotlib to function correctly

#venv (built in python3)

create:
```
python3 -m venv env
```
activate:
```
source env/bin/activate
```
deactivate:
```
deactivate
```

#virtualenv

initiation:
``` 
pip install virtualenv virtualenvwrapper
nano ~/.bash_profile
```

```
# ****In File Add
# Virtualenv/VirtualenvWrapper
source /usr/local/bin/virtualenvwrapper.sh
```

```
source ~/.bash_profile
```

create:
```
mkvirtualenv cv -p python3
```

activate:
```
works cv
```
deactivate:
```
deactivate
```
