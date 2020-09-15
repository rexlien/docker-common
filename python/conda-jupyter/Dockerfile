FROM continuumio/miniconda

ENV TZ=Asia/Taipei
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

WORKDIR /work
VOLUME /work/data

EXPOSE 8888

SHELL ["/bin/bash", "-c"]
COPY env.yaml env.yaml
RUN conda env create -f env.yaml
RUN echo "source activate ml" > ~/.bashrc
ENV PATH /opt/conda/envs/env/bin:$PATH
ARG ML_SRC=src

COPY ${ML_SRC} src

CMD ["conda", "run", "-n", "ml", "jupyter", "notebook", "--ip=0.0.0.0", "--port=8888", "--no-browser", "--allow-root", "--NotebookApp.token=''", "--NotebookApp.password=''"]
