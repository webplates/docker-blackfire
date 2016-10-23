# Blackfire CLI Docker image

**Docker image for profiling PHP CLI scripts.**

The image comes with Blackfire CLI and Blackfire PHP Probe extension installed, created from official PHP Docker images.

Currently supported PHP versions:

- 5.6
- 7.0


## Install

Via Composer

``` bash
$ docker pull webplates/blackfire-cli
```


## Usage

First of all you need to get your Client credentials from https://blackfire.io/account.

You can then pass them as environment variables to the Blackfire client and run your script in a container:

``` bash
$ export BLACKFIRE_CLIENT_ID=XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX
$ export BLACKFIRE_CLIENT_TOKEN=XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
$ docker run --rm -t -v "$PWD":/app -e BLACKFIRE_CLIENT_ID=$BLACKFIRE_CLIENT_ID -e BLACKFIRE_CLIENT_TOKEN=$BLACKFIRE_CLIENT_TOKEN webplates/blackfire-cli blackfire run php script.php
```

If you want a more permanent solution, add the following to your shell config (`.bashrc`, `.zshrc`, etc):

``` bash
export BLACKFIRE_CLIENT_ID=XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX
export BLACKFIRE_CLIENT_TOKEN=XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
alias bf='docker run --rm -t -v "$PWD":/app -e BLACKFIRE_CLIENT_ID=$BLACKFIRE_CLIENT_ID -e BLACKFIRE_CLIENT_TOKEN=$BLACKFIRE_CLIENT_TOKEN webplates/blackfire-cli blackfire run php'
```

Then simply do `bf script.php`.

**Note:** since volume mapping is used to get the files inside the container, it only works when called from the project root, it cannot access parent directories.


To see how CLI profiling with Blackfire works check the [official documentation](https://blackfire.io/docs/cookbooks/profiling-cli).


## License

The MIT License (MIT). Please see [License File](LICENSE) for more information.
