# Keeping API Keys Around Safely

API keys are kept in a key file with a key name and an encrypted API key.  This is useful if you are
testing with a variety of API keys.

The following scripts are written in bash.

* `encrypt_keys`.  This script will read the `~/keys` file and encrypt all unencrypted API keys.

* `get_key` returns a decrypted key specified by key name from `~/keys`.

* `set_key` sets the environment variable `API_KEY` to a key specified by the key name.
Because it sets an environment variable, it needs to be `source`ed.

* `which_key` informs which key is set in the environment variable `API_KEY`.

## What is used to Encrypt and Decrypt?

Encryption and decryption is done via Ionic Security's 
[machina CLI tool](https://dev.ionic.com/tools/machina). But before you can use `machina`, you need to
set up a free account and enroll your device.

To set a free account, go [here](https://ionic.com/start-for-free/).  Follow the directions and run
through the JavaScript HelloWorld tutorial.  **Note** your login, password, and keyspace.

Now you need to download machina.  Go to the [machina webpage](https://dev.ionic.com/tools/machina) and
click on the "Show Install Instructions" button. Click on either "linux" or "macos" icons and follow
the download directions.  The Ionic Security's tool section assists you in creating CLI commands.

Since you'll be running in a Linux or MacOS terminal, you will need to enroll your device.  This is
done with the [`machina profile enroll`](https://dev.ionic.com/tools/machina/profile_enroll) command.
Set devicetype to `default`.  Key in your email address you used to register and your keyspace into
the form.  On the left, copy the text and exceute in a CLI window. You will be asked for password.
And now you have your device enrolled.

Now you're ready to use the scripts.

Create a `~/keys` file in the following this template `<key_name>, <API key>`, for example:

```
acme_us, 8bN0pLNqwxc
acme_eu, 65M1sFHMz5r
chojo_asia, Rvb93ixlpQ2kjh5
```
Run `encrypt_keys` to encrypt them.  You can add new keys at a later time and run `encrypt_keys` again.
The script will only encrupt the unencrypted keys.

To fetch key and set the `API_KEY`, do: `source set_key chojo_asia`.  Feel free to change `API_KEY` to
`ACME_API_KEY` to be more specific.

## Why Encrypt and Decrypt using Ionic Security?
Ionic Security allows you to set policy on each key.  If you wanted, you could have one key file and
set up pollicies to share the keys with different groups.  There is a policy tutorial in Ionic
Security's [tutorials](https://dev.ionic.com/tutorials).

These scripts were based off of an Ionic Security
[Source Control Hooks tutorial](https://dev.ionic.com/tutorials/sdk-advanced/source-control).
