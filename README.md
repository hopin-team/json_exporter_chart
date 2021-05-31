# json_exporter_chart

Helm chart for the [Prometheus JSON Exporter](https://github.com/prometheus-community/json_exporter).
It's ready to receive a ConfigMap as the json_exporter configuration. However since a secret may be needed in the configuration, the chart can read the config from a Secret instead of the ConfigMap as described [here](https://github.com/hopin-team/json_exporter_chart/blob/main/templates/deployment.yaml#L69):
```
      {{- if .Values.configSecretMount.enabled }}
      - secret:
          secretName: {{ .Values.configSecretMount.secret.secretName }}
          defaultMode: {{ .Values.configSecretMount.secret.defaultMode }}
      {{- else }}
      - configMap:
          defaultMode: 420
          name: {{ template "prometheus-json-exporter.fullname" . }}
      {{- end }}
```
