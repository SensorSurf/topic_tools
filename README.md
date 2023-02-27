# topic_tools

This is a simplified version of the topic_tools package available [here](https://github.com/ros-tooling/topic_tools). We created a reduced set to give credit to the authors while only exposing the interfaces useful to our application.

### Throttle

Throttle is ROS 2 node that subscribes to a topic and republishes incoming data to another topic, either at a maximum bandwidth or maximum message rate.

#### Usage

#### throttle message (rate)

```
ros2 run topic_tools throttle messages <intopic> <msgs_per_sec> [outtopic]
```

Throttle messages on `intopic` to a particular rate.
- `intopic`: Incoming topic to subscribe to
- `msgs_per_sec`: maximum messages per second to let through.
- `outtopic`: Outgoing topic to publish on (default: intopic_throttle)

E.g. throttle bandwidth-hogging laser scans (base_scan) to 1Hz:

```
ros2 run topic_tools throttle messages base_scan 1.0
```

#### throttle bytes (bandwidth)

```
ros2 run topic_tools throttle bytes <intopic> <bytes_per_sec> <window> [outtopic]
```

Throttle messages on `intopic` to a particular rate.
- `intopic`: Incoming topic to subscribe to
- `msgs_per_sec`: maximum messages per second to let through.
- `outtopic`: Outgoing topic to publish on (default: intopic_throttle)

E.g. throttle bandwidth-hogging laser scans (base_scan) to 1KBps:

```
ros2 run topic_tools throttle bytes base_scan 1024 1.0
```

#### Parameters

- `input_topic` (string)
    - the same as if provided as a command line argument
- `output_topic` (string, default=`<input_topic>_throttle`)
    - the same as if provided as a command line argument
- `lazy` (bool, default=False)
    - If True, only subscribe to `input_topic` if there is at least one subscriber on the `output_topic`
- `use_wall_clock` (bool, default=False)
    - If True, then perform all rate measurements against wall clock time, regardless of whether simulation / log time is in effect.
