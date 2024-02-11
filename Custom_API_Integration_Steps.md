### Create Splunk App from UI


### Add below stanza to custom_api_data/default/app.conf

```bash
[package]
id = custom_api_data
```

### $SPLUNK_HOME/etc/apps/custom_api_data/bin/getCustomAPIData.py

```bash
from __future__ import print_function
from builtins import str
import sys
import xml.dom.minidom, xml.sax.saxutils

# Empty introspection routine
def do_scheme():
    pass

# Empty validation routine. This routine is optional.
def validate_arguments():
    pass

# Routine to get the value of an input
def get_who():
    try:
        # read everything from stdin
        config_str = sys.stdin.read()

        # parse the config XML
        doc = xml.dom.minidom.parseString(config_str)
        root = doc.documentElement
        conf_node = root.getElementsByTagName("configuration")[0]
        if conf_node:
            stanza = conf_node.getElementsByTagName("stanza")[0]
            if stanza:
                stanza_name = stanza.getAttribute("name")
                if stanza_name:
                    params = stanza.getElementsByTagName("param")
                    for param in params:
                        param_name = param.getAttribute("name")
                        if param_name and param.firstChild and \
                           param.firstChild.nodeType == param.firstChild.TEXT_NODE and \
                           param_name == "who":
                            return param.firstChild.data
    except Exception as e:
        raise Exception("Error getting Splunk configuration via STDIN: %s" % str(e))

    return ""

# Routine to index data
def run_script():
    print("hello world, %s!" % get_who())

# Script must implement these args: scheme, validate-arguments
if __name__ == '__main__':
    if len(sys.argv) > 1:
        if sys.argv[1] == "--scheme":
            do_scheme()
        elif sys.argv[1] == "--validate-arguments":
            validate_arguments()
        else:
            pass
    else:
        run_script()

    sys.exit(0)

```

### inputs.conf.spec 

```bash
[getCustomAPIData://default]
key = <value>
disabled = <value>
sourcetype = <value>
interval = <value>

```

### props.conf

```bash
[_json]
TRUNCATE = 9999999
```

### example code snippet get the data from API 

```bash
# Routine to index data
def run_script():
    url = "https://api.github.com/repos/SoftManiaTech/splunk_cluster_admin_training/commits"
    headers = {
    'Accept': 'application/vnd.github+json',
    'Authorization': 'Bearer <token>',
    'X-GitHub-Api-Version': '2022-11-28'
    }
    response = requests.request("GET", url, headers=headers)
    return response.text

```

```bash
def get_data_from_API():
    # print(get_who())
    response_data = json.loads(run_script())
    for data in response_data:
        print(json.dumps(data))
```
