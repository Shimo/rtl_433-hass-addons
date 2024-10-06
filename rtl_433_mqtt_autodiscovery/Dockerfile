ARG BUILD_FROM=ghcr.io/home-assistant/amd64-base-python:3.12-alpine3.19
FROM ${BUILD_FROM} as builder

ARG rtl433GitRevision=23.11

RUN wget https://github.com/Shimo/rtl_433-hass-addons-Custom-added-reed_open/blob/main/rtl_433_mqtt_autodiscovery/rtl_433_mqtt_hass.py -O rtl_433_mqtt_hass.py

FROM ${BUILD_FROM}

COPY --from=builder rtl_433_mqtt_hass.py .
COPY run.sh .

RUN \
    pip install \
        --no-cache-dir \
        --prefer-binary \
        paho-mqtt==1.6.1 \
    \
    && chmod a+x /run.sh

CMD [ "/run.sh" ]
