FROM python:3.7
ARG REDSHIFT_IAM_ROLE
ARG REDSHIFT_HOST
ARG REDSHIFT_PORT
ARG REDSHIFT_USERNAME
ARG REDSHIFT_PASSWORD
ARG DATA_LAKE
ARG DATA_LAKE_TYPE
ARG DATA_LAKE_ROOT_PATH
ARG TENANT
ARG STAGE
ENV REDSHIFT_IAM_ROLE=$REDSHIFT_IAM_ROLE \
REDSHIFT_HOST=$REDSHIFT_HOST \
REDSHIFT_PORT=$REDSHIFT_PORT \
REDSHIFT_USERNAME=$REDSHIFT_USERNAME \
REDSHIFT_PASSWORD=$REDSHIFT_PASSWORD \
DATA_LAKE=$DATA_LAKE \
DATA_LAKE_TYPE=$DATA_LAKE_TYPE \
DATA_LAKE_ROOT_PATH=$DATA_LAKE_ROOT_PATH \
TENANT=$TENANT \
STAGE=$STAGE
COPY requirements.txt /tmp/requirements.txt
RUN pip install -r /tmp/requirements.txt

# ----------------------------------------
# Non-Root User Creation!
# ----------------------------------------
ARG PEAK_USER_ID
ENV PEAK_USER_ID=$PEAK_USER_ID
# Add a new user, this must have the UserId of PEAK_USER_ID
RUN useradd -m -d /home/peak-user -u $PEAK_USER_ID peak-user

# Give the new user the permissions to the directory that it might need
RUN chown -R peak-user:peak-user /home/peak-user

# Set the working directory
WORKDIR /home/peak-user

# Set the user as default for the container
USER $PEAK_USER_ID