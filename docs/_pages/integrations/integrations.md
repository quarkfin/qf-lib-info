---
permalink: /integrations/
title: "Integrations"
toc: true
toc_sticky: true
toc_label: "On this page"
toc_icon: "cog"
---

This document describes the basic Integrations

# Overview
AAAAAAAAAAAAAAAAAAAA

```python
class CustomTimeEvent (TimeEvent):
    def notify(self, listener) -> None:
        listener.on_custom_event()

class CustomTimeEventListener:
    def on_custom_event(self):
        ...
```


```python
start_time = {
    "hour": 13, "minute": 20,
    "second": 0, "microsecond": 0
}
end_time = {
    "hour": 16, "minute": 0,
    "second": 0, "microsecond": 0
}
frequency = Frequency.MIN_30
```

