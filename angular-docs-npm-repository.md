# NPM Repository

The VisuallyJs packages are hosted in two places:

* In the public NPM repository (<https://registry.npmjs.org>) there is a watermarked version of each package which can be used for evaluation and for users who satisfy the conditions of non-commercial usage.
* For licensees, the packages are hosted in our private VisuallyJs NPM repository. This repository is available to all licensees who currently have access to download new releases.

## Repository URL[​](#repository-url "Direct link to Repository URL")

Note the trailing slash on the repository location: this must be included.

```javascript
https://download.jsplumbtoolkit.com/repository/visuallyjs/

```

## Logon[​](#logon "Direct link to Logon")

To login to the VisuallyJs NPM repository you use your licensee ID:

```bash
npm adduser --registry=https://download.jsplumbtoolkit.com/repository/visuallyjs/
...
Username:  <licensee id>
Password: <...>

```

Your password will have been supplied in an email from VisuallyJs.

## .npmrc Setup[​](#npmrc-setup "Direct link to .npmrc Setup")

You'll need to map the `@visuallyjs` scope to VisuallyJs's NPM repository. For that, ensure your `.npmrc` has this entry:

```bash
@visuallyjs:registry=https://download.jsplumbtoolkit.com/repository/visuallyjs/

```

## Tokens[​](#tokens "Direct link to Tokens")

Running the `npm adduser` command to login to the NPM repository will result in an `authToken` being written to your local `.npmrc`. For licensees, the number of active tokens is determined relative to the number of developer seats purchased: for single seat licensees, one token is supported. For holders of a small team (1-5 developers) license, 6 concurrent tokens are supported. For holders of a team (1-10 developers) license, 12 concurrent tokens are supported. The extra token(s) are intended to help if you have a machine that runs automated builds or some such setup. For holders of an unlimited seats developer license, unlimited NPM tokens are supported.

## Repository Availability[​](#repository-availability "Direct link to Repository Availability")

Whilst every effort is made to ensure the repository is available at all times, **VisuallyJs enters into no Service Level Agreement with licensees as to the availability of the NPM repository**. It is recommended that all licensees download the VisuallyJs packages from our [Downloads Page](https://visuallyjs.com/download), and/or configure a repository that proxies our repository (such as JFrog - instructions given below).

***

## JFrog Setup[​](#jfrog-setup "Direct link to JFrog Setup")

You can

To use JFrog to serve VisuallyJs packages you need to setup both a **remote** repository and a **virtual** repository. The remote repository acs as the proxy to our repository, and the virtual repository rewrites the download URLs that our reposut

The steps you need to follow are:

1. ### Generate a token[​](#generate-a-token "Direct link to Generate a token")

Generate a token on the VisuallyJs NPM repository using the Logon instructions above. The token is written to your .npmrc file in this format:

```bash
//download.jsplumbtoolkit.com/repository/visuallyjs/:_authToken=89efb562-f762-adb1-fefe-9834fe32

```

2. ### Create remote repository in JFrog[​](#create-remote-repository-in-jfrog "Direct link to Create remote repository in JFrog")

![Remote repository config](https://static.visuallyjs.com/img/npm-repository/jfrog/1-create-remote-repository.png)

Select `NPM` as the repository type. Then enter these details:

* URL: <https://download.jsplumbtoolkit.com/repository/visuallyjs/>
* User Name: (your licensee ID)
* Password/Access Token: 89efb562-f762-adb1-fefe-9834fe32 (in this example - its the token shown from the .npmrc above)
* Enable Token Authentication: checked

![Remote repository config](https://static.visuallyjs.com/img/npm-repository/jfrog/2-configure-remote-repository.png)

When you click the 'Test Connection' button you should see a dialog confirming a successful connection:

![Remote repository connect](https://static.visuallyjs.com/img/npm-repository/jfrog/3-connect-success.png)

Your remote repository is now setup - it can proxy requests to our NPM repository. Press `Create Remote Repository` to finalise it. Now click on **Set Up npm Client**.

3. ### Get client config instructions[​](#get-client-config-instructions "Direct link to Get client config instructions")

Enter your JFrog password and click on **Generate Token & Create Instructions**:

![Generate NPM token](https://static.visuallyjs.com/img/npm-repository/jfrog/4-generate-token.png)

4. ### Get .npmrc instructions[​](#get-npmrc-instructions "Direct link to Get .npmrc instructions")

Once the token has been created, scroll down to the **Edit .npmrc (scoped)** section. VisuallyJs is a scoped NPM package.

![Remote repository connect](https://static.visuallyjs.com/img/npm-repository/jfrog/5-npmrc-instructions.png)

7. ### Edit your .npmrc[​](#edit-your-npmrc "Direct link to Edit your .npmrc")

Lastly, edit your .npmrc to include the instructions JFrog supplied - the url to the registry to use, and the JFrog auth token:

```shell
@visuallyjs:registry=https://YOUR-HOST.jfrog.io/artifactory/api/npm/visuallyjs/

//YOUR-HOST.jfrog.io/artifactory/api/npm/visuallyjs/:_authToken=cmVmdGtuOjAxOjE4MjE3Mzg4OTM6R1Z5R292SFJaNHR6ckFWaVN1ZjAxT1BlOHpv


```

8. ### Verifying your setup[​](#verifying-your-setup "Direct link to Verifying your setup")

You can verify this is all setup correctly by running an `npm view` command:

```shell
npm view @visuallyjs/browser-ui@latest

```

You should see output like this:

```shell
@visuallyjs/browser-ui@1.2.9 | Commercial | deps: none | versions: 18
VisuallyJs
https://visuallyjs.com/

dist
.tarball: https://YOUR-HOST.jfrog.io/artifactory/api/npm/visuallyjs/@visuallyjs/browser-ui/-/1.2.9.tgz
.shasum: a5dcc4043c21fd8650c4512d1ef53660c04cf71e
.integrity: sha512-Vo5Rrv9CnjokUX9riKFGTEznPB/tAc24tg4THXTdRBq+H86iMAvP864H9j5j3NBn6q3pShcV22Jn7fK7idVpFA==

dist-tags:
latest: 1.2.9  

published yesterday


```
