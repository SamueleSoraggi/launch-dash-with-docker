FROM dreg.cloud.sdu.dk/ucloud-apps/jupyter-base:3.4.2

MAINTAINER "Samuele Soraggi <samuele@birc.au.dk>"

LABEL software="Genomics Sandbox" \
      author="Samuele Soraggi" \
      version="2022.08.01" \
      license="MIT" \
      description="Courses, datasets and software tools for genomics analysis"

USER 11042

## Set startup script in the PATH
COPY --chown="${NB_USER}":"${NB_GID}" dashboard /usr/dashboard
RUN fix-permissions /usr/dashboard \
  && mamba env create -p "${CONDA_DIR}/envs/arg_dashboard" -f /usr/dashboard/environment.yml \
  && fix-permissions "${CONDA_DIR}" \
  && ${CONDA_DIR}/envs/arg_dashboard/bin/python -m ipykernel install --user --name="arg_dashboard" --display-name "arg_dashboard"


WORKDIR /usr/dashboard

EXPOSE 8850

## Set startup script in the PATH
COPY --chown="${NB_USER}":"${NB_GID}" start-jupyter "${CONDA_DIR}"/bin/
RUN chmod +x "${CONDA_DIR}"/bin/start-jupyter \
  && fix-permissions /home/ucloud