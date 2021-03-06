# chameleon-client


This client script provides an automated way to create a lease and start an instance in Chameleon. New users may want to use the Chameleon website instead for this. For documentation on how to use Chameleon, please take a look at the [Getting Started](https://chameleoncloud.readthedocs.io/en/latest/getting-started/index.html) documentation.

To be added to the SAGE project in Chameleon, please send an email with your Chameleon username to (email address not decided yet) . 



##  OpenStack RC File
Once you created Chameleon user account and have been added to the SAGE project in Chameleon, download the OpenStack RC File. Go to [https://chi.uc.chameleoncloud.org/project/](https://chi.uc.chameleoncloud.org/project/). Click on your username in the top right corner of the web site and select "OpenStack RC File v3". Save that file somewhere on your machines, for example in your home directory like this: `${HOME}/SAGE_project-openrc.sh`

## ssh key
Upload an existing public key or create a new ssh key pair: Goto [https://chi.uc.chameleoncloud.org/project/key_pairs](https://chi.uc.chameleoncloud.org/project/key_pairs) and click on either "Import Public Key" or "Create Key Pair". You will need the private key to be able to ssh into an instance you created. They default place for a private key is `~/.ssh/id_rsa`. If have more than one ssh key you can also use a more descriptive names such as  `~/.ssh/chameleon.pem` and `~/.ssh/chameleon.pub`.


## Build container

```bash
docker build -t chameleon-client .
```

## Start container
```bash
docker run -ti --rm -v ${HOME}/SAGE_project-openrc.sh:/openrc.sh:ro chameleon-client /bin/bash
```

On start of the container your `openrc.sh` will be automatically sourced. Be sure to specify the correct path to that file in the `docker run` command. Note that the openrc.sh will ask you for your chameleon password every time you start the container.

## Start chameleon bare-metal instance

```bash
./create_instance.sh
```

By default the leasing lasts within a day. If longer leasing day is needed,
```bash
./create_instance.sh -help
 Lease a Chameleon node
 USAGE: create_instance.sh [OPTIONS]
    [OPTIONS]
    -help         Print help
    -days         Number of days to lease
./create_instance.sh -days 7
```

You can change some defaults by setting environment variables, e.g.:
```bash
export IMAGE='CC-Ubuntu18.04-CUDA10'
export KEY_NAME='my_favorite_ssh_key'  # e.g. if you have more than one key in Chameleon
```
