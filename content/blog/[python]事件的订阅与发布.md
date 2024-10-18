---
title: [python]事件的订阅与发布
date: 2024-10-18T03:16:19.162Z
---

# 事件的订阅与发布
## 事件枚举
```python
from enum import Enum

class EventTypes(Enum):
    Event1="event1"
    Event2 = "event2"
    ...
```
## 事件发布
全局单例
```python
class EventPublisher:
    def __init__(self):
        self._subscribers = []
 
    def add_subscriber(self, subscriber):
        self._subscribers.append(subscriber)
 
    def remove_subscriber(self, subscriber):
        self._subscribers.remove(subscriber)
 
    def publish_event(self, event_type, event_data=None):
        for subscriber in self._subscribers:
            subscriber.handle_event(event_type, event_data)

event_publisher = EventPublisher()
```

## 事件订阅
抽象父类
```python
from abc import ABC, abstractmethod

class EventSubscriber(ABC):
    @abstractmethod
    def handle_event(self, event_type, event_data=None):
        ...
```
具体子类
```python
from event_subscriber import EventSubscriber
from event_types import EventTypes

class App(EventSubscriber):
    def __init__(self) -> None:
        event_publisher.add_subscriber(self)
        ...
    def handle_event(self, event_type, event_data=None):
        if event_type == EventTypes.Event1:
            ...
        if event_type == EventTypes.Event2:
            ...
```
