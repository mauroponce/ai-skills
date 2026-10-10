# Observability

Load when diagnosis, async work, integration failure, or release verification depends on runtime signals. Prefer existing metrics, traces, structured logs, error reporting, queue dashboards, and deploy annotations. Connect a signal to a request/job, version, time window, and affected user path. Avoid new instrumentation when existing evidence answers the question. Any added signal should support a concrete decision or alert, avoid secrets/personal data, and be cheap enough for its traffic volume.
