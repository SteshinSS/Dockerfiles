# syntax=docker/dockerfile:1

FROM pytorch/pytorch:1.9.0-cuda11.1-cudnn8-runtime


# Initial apt-get
RUN apt-get update && apt-get install -y \
	git \
	vim \
	sudo \
    wget


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
    && pip3 install --user --upgrade numpy scipy matplotlib ipython jupyterlab jupyter pandas scikit-learn seaborn requests pytest pylint \
    && pip3 install --user --upgrade wandb gensim spacy nltk \
    && python -m ipykernel install --user --display-name ipykernel

RUN pip3 install --user torch==1.9.0+cu111 torchvision==0.10.0+cu111 torchaudio==0.9.0 -f https://download.pytorch.org/whl/torch_stable.html


# Install xonsh
RUN pip3 install 'xonsh[full]' \
    && echo \$PROMPT = \'{env_name}{BOLD_PURPLE}{user}{WHITE}-{localtime}:{cwd}--\> \' > .xonshrc


EXPOSE 8888:8888
CMD ["xonsh"] 
