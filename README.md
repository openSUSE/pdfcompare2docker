# pdfcompare2docker

Use the pdfcompare tool, despite it not having been updated past Python 2
WITH THIS ONE WEIRD TRICK!

## Installing

1. Install Docker and docker-compose on your distribution.
   *  OpenSUSE/SLES: `sudo zypper install docker python3-docker-compose`

2. Clone this repository: `git clone https://github.com/openSUSE/pdfcompare2docker`


### First-Run Prerequisites

On the first run, Docker needs to download a container with an installation of `pdfcompare` on openSUSE Leap 15.1.

This means, you need:

*  Make sure you have at least 400 MB of space on your root partition left
*  Make sure you have internet access
*  Either have the root password of your machine at the ready or add your user account to the `docker` group (after adding your user account to the group you need to log out and back in again before the group change is applied)
*  The `docker` service must be running: `sudo systemctl start docker`


### Creating Output Documents

1. In a terminal, go to the cloned directory.
2. Copy both PDFs to the cloned directory: `cp /path/to/PDF1.pdf /path/to/PDF2.pdf .`
   Make sure none of the files you want to compare is called `output.pdf`.
3. Run `docker-compose`:
   * If your user account is a member of the `docker` group: `docker-compose run pdfcompare PDF1.pdf PDF2.pdf`
   * If your user account is not a member of the `docker` group: `sudo docker-compose run pdfcompare PDF1.pdf PDF2.pdf`

(Other options of the script are explained by the tool itself, using `docker-compose run pdfcompare --help`.)

NOTE: If one of the PDFs you want to diff has an appended `.old` or a date like `-20220209` (for example, `MyBook.pdf-20220209`) this causes `pdfcompare` to mark all content as changed. Make sure the PDFs to compare end in `.pdf` only.    

## References

* For the container image itself, see [Docker Hub](https://hub.docker.com/r/susedoc/pdfcompare).
* For the container definition, see [the doc-ci repository](https://github.com/openSUSE/doc-ci/tree/develop/build-pdfcompare-container).
