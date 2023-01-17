FROM dreg.cloud.sdu.dk/ucloud-apps/jupyter-base:3.4.2

MAINTAINER "Samuele Soraggi <samuele@birc.au.dk>"

LABEL software="Genomics Sandbox" \
      author="Samuele Soraggi" \
      version="2022.08.01" \
      license="MIT" \
      description="Courses, datasets and software tools for genomics analysis"

USER 0

## Set startup script in the PATH
COPY --chown="${NB_USER}":"${NB_GID}" dashboard/ /usr/dashboard
RUN fix-permissions /usr/dashboard \
  && pip install -r /usr/dashboard/requirements.txt

USER 11042

WORKDIR /usr/dashboard

CMD gunicorn -b 0.0.0.0:80 arg_dashboard:server

