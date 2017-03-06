Python 3
--------
```
git clone https://github.com/robinchew/pwg-tutorial.git
virtualenv3 ~/venv3
~/venv3/bin/pip install sphinx
source ~/venv3/bin/activate
cd pwg-tutorial
make html
```
Open `_build/html/index.html` in browser.

Installing Sphinx with **Python 2** requires Jinja to be installed separately (`pip install jinja`).
