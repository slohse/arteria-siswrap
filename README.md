Arteria Siswrap
===============
A self contained (Tornado) REST service for managing running of external [Sisyphus](https://github.com/Molmed/Sisyphus)
commands such as the quick report generator and quality control suite.


Development and usage examples
------------------------------

To make development on this service easier a [Vagrant](https://www.vagrantup.com/) environment is provided.
Here are some brief notes on how to get it working.

```
# ------------------
# Setup vagrant env
# ------------------
vagrant up

# ------------------
# Prepare environment
# ------------------
vagrant ssh
cd /vagrant
virtualenv venv
source venv/bin/activate
pip install -e .
pip install -r requirements/dev

# ------------------
# Run unit tests
# ------------------
py.test tests/unit/*.py

# ------------------
# Run service to test it
# ------------------
siswrap-ws --configroot config/ --port 10900 --debug


# Example 1: To get a overview of the api run:
curl http://localhost:10900/api | python -m json.tool

# Example 2: To start a index checking job run
curl -X POST --data '{"runfolder":"160824_M00485_0293_000000000-ALRHK"}' localhost:10900/api/1.0/checkindices/run/160824_M00485_0293_000000000-ALRHK

# Example 3: To check the status a job, query the link returned when starting it, e.g.
curl http://localhost:10900/api/1.0/checkindices/status/<job_id>

```
