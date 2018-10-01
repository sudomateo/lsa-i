# Packages

In Linux, software is installed by installing packages. Packages are nothing more than an archive of files that contain software. These archives of files come in different formats depending on the Linux distribution you are running.

## Package Formats

Some of the common package formats are listed below.

| Format    | Name                  | Operating System                 |
| --------- | --------------------- | -------------------------------- |
| `.rpm`    | RPM Package Manager   | CentOS, RedHat, Fedora, openSUSE |
| `.deb`    | Debian Package Format | Debian, Ubuntu                   |
| `.tar.gz` | Tar Gzip Files        | Any                              |

These package formats are not interchangeable. You cannot, and should not, attempt to install a `.rpm` package on a Debian system and vice versa.

## Package Managers

In addition to package formats, there are tools that are used to install these packages. These tools are often called package managers and they are detailed below.

| Package Manager | Operating System       |
| --------------- | ---------------------- |
| `yum`           | CentOS, RedHat, Fedora |
| `rpm`           | CentOS, RedHat, Fedora |
| `dnf`           | Fedora                 |
| `apt-get`       | Debian, Ubuntu         |
| `apt`           | Debian, Ubuntu         |
| `aptitude`      | Debian, Ubuntu         |
| `zypper`        | openSUSE               |

## Package Naming

Packages usually have a naming convention so that the user installing the package knows which version of the package is being installed. This naming convention can vary between package formats but generally follows a similar pattern.

### RPM Package Naming

RPM packages tend to follow this naming convention.

* `package-a.b.c-x.arch.rpm`
    * `package` is the name of the package.
    *  `a.b.c` is the version number.
    * `x` is the build number.
    * `arch` is the architecture (x86_64).
    * `rpm` is the RPM package format.

!!! example "Example: Showing a version of a package"

    This is what an RPM package name looks like. The `el7.centos` is just a more specific naming convention for packages that are created for multiple operating system versions.

    ```
    vim-enhanced-7.4.160-4.el7.x86_64.rpm
    ```

## Installing Packages

Packages are installed using a packager manager. Depending on your operating system the package manager may be different.

### `rpm`

The `rpm` command is used to manage RPM packages. It's not really common to use anymore since the `yum` command took over. However, it's still a good command to learn.

!!! example "Example: Usage of `rpm`."

    Install a package.

    ```
    $ sudo rpm -i vim-enhanced-7.4.160-4.el7.x86_64.rpm
    ```

    Remove a package.

    ```
    $ sudo rpm -e vim-enhanced-7.4.160-4.el7.x86_64.rpm
    ```

### `yum`

The `yum` command is another package manager that manages RPM packages. `yum` allows you to do many more operations than `rpm` such as search for, download, install, and remove packages.

!!! example "Example: Usage of `yum`."

    Install a package.

    ```
    $ sudo yum install vim-enhanced
    ```

    Remove a package.

    ```
    $ sudo yum remove vim-enhanced
    ```

    Update all installed packages.

    ```
    $ sudo yum update
    ```

    List all available packages.

    ```
    $ sudo yum list
    ```

    List all installed packages.

    ```
    $ sudo yum list installed
    ```

    Find a package that contains the `vim` command.

    ```
    $ sudo yum provides vim
    ```

    Search for a package with `vim` in its name.

    ```
    $ sudo yum search vim
    ```

    Gather information about the `vim-enhanced` package.

    ```
    $ sudo yum info vim-enhanced
    ```

## Finding Packages

We've already covered how to download and install packages using the `yum` command in the previous section, but how did Linux know where to download these packages?

Linux packages are normally located in a repository, or repo. A repository is nothing more than a collection of software packages that are served over HTTP or FTP. Most repositories in the Linux community are public such as the [CentOS 7 repository](http://mirror.centos.org/centos/7/os/x86_64/Packages/).

The packages in these public repositories are cryptographically signed by the package maintainers and then distributed and verified upon installation. Packages will not be installed if this verification fails.

You can add new repositories to Linux so that you can install new packages that do not come with your Linux distribution by default. The way to add a repository on CentOS 7 is to add a file to the `/etc/yum.repos.d` directory. Although adding repositories is outside the scope of this course, it is definitely something to learn.
