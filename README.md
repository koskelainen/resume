
### Quick start

Get started quickly using [Overleaf](https://www.overleaf.com/latex/templates) template.

### Requirements


First, add your local user to docker group (should already be the case):
```bash
sudo usermod -aG docker YOURUSERNAME
```

The `\<your project>\*.sh` will use your current user and group id to compile.

### Build using Docker

```bash
# Change to your project
cd cv_latex

# Build docker image 
docker build -t latex:ubuntu .
```


Compile latex sources using docker:
```bash
# make it executable
chmod +x latexdockercmd.sh

# Optional: Change the version (see above, default latex:ubuntu)
edit ./latexdockercmd.sh

# Compile using pdflatex (docker will pull the image automatically)
./latexdockercmd.sh pdflatex koskelainen.tex

# Or use latexmk (best option)
./latexdockercmd.sh latexmk -cd -f -interaction=batchmode -pdf koskelainen.tex


# Or make multiple passes (does not start container twice)
./latexdockercmd.sh /bin/sh -c "pdflatex koskelainen.tex && pdflatex koskelainen.tex"
```

### Daemon setup


If you're working on source in latex, you might want to compile it multiple times and don't want to start a container each time.

```bash
# Start a daemon container on this path, it accepts commands from latexdockerdaemoncmd.sh
./latexdockerdaemon.sh

# Execute the command in the daemon container, only the daemon container is running
./latexdockerdaemoncmd.sh pdflatex koskelainen.tex

# Stop the daemon
docker stop latex_daemon
```

### Clean

```bash
rm -rf *.aux *.log *.out *.fdb_latexmk *.fls
find . -maxdepth 1 -regextype posix-extended -regex '.*/file[1-9]{2,3}.txt' -delete

```

### Source

- [Sourabh Bajaj](https://github.com/sb2nov/resume)
- [Benedikt Lang](https://github.com/blang/latex-docker/)

Thank you so much for your help.
