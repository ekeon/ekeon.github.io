---
layout: post
title:  "python-jekyll-push-script"
date:   2016-02-24 4:35
categories: jekyll update
---
<a href="http://halryang.net/push-jekyll-simply-with-python-script/">참고블로그</a>

```python
import sys
reload(sys)

sys.setdefaultencoding('utf-8')

import subprocess
import os

os.chdir('/path')

subprocess.call(["git", "add", "."])
subprocess.call(["git", "commit", "-m", "auto push"])
subprocess.call(["git", "push", "-u", "origin", "master"])

```