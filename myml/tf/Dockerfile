# syntax=docker/dockerfile:1

FROM tensorflow/tensorflow:latest-gpu


# Initial apt-get
RUN apt-get update && apt-get install -y \
	git \
	vim \
	sudo


# Create a sudo user myml
RUN groupadd -r -g 1000 myml \
    && useradd --system --create-home -u 1000 -g 1000 myml \
    && usermod -aG sudo myml
USER myml
ENV USER=myml


# Update .bashrc
WORKDIR /home/myml
ENV PATH="/home/myml/.local/bin:${PATH}"


# Install packages
RUN python -m pip install --upgrade pip \
    && pip3 install --user --upgrade numpy scipy matplotlib ipython jupyterlab jupyter pandas scikit-learn seaborn requests pytest pylint wandb \
    && python -m ipykernel install --user --display-name ipykernel

RUN pip3 install --user --upgrade tensorflow-hub tensorflow-datasets tensorflow-model-optimization tensorflow-lattice tensorflow-probability tensorflow-io tensorflow-cloud tensorflow-text tfx


# Install xonsh
RUN pip3 install 'xonsh[full]' \
    && echo \$PROMPT = \'{env_name}{BOLD_PURPLE}{user}{WHITE}-{localtime}:{cwd}--\> \' > .xonshrc


EXPOSE 8888:8888
CMD ["xonsh"] 
