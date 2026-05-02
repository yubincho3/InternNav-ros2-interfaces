# InternNav-ros2-interfaces

Custom ROS 2 message definitions shared across the InternNav server and client workspaces.

## Package

| Package | Build Type |
|---------|------------|
| `internnav_interfaces` | ament_cmake |

## Messages

### `DiscreteStamped.msg`

Carries a sequence of discrete navigation actions with a timestamp.

```
uint8 STOP       = 0
uint8 FORWARD    = 1
uint8 TURN_LEFT  = 2
uint8 TURN_RIGHT = 3
uint8 LOOK_DOWN  = 5

std_msgs/Header header     # stamp = image capture timestamp, frame_id=''
uint8[] actions            # ordered array of discrete action values
```

**Action semantics**

| Value | Constant | Meaning |
|-------|----------|---------|
| 0 | `STOP` | Halt all motion |
| 1 | `FORWARD` | Move forward ~0.25 m |
| 2 | `TURN_LEFT` | Rotate left |
| 3 | `TURN_RIGHT` | Rotate right |
| 5 | `LOOK_DOWN` | Tilt camera downward |

**Publishers / Subscribers**

| Node | Role |
|------|------|
| `internnav_system2` (`InternNav-ros2-server`) | Publisher — outputs parsed LLM actions |
| `internnav_system1` (`InternNav-ros2-server`) | Subscriber — uses actions to trigger planning reset |
| `internnav_planner` (`InternNav-ros2-client`) | Subscriber — converts actions to robot motion commands |

> This workspace must be built and sourced **before** building `InternNav-ros2-server` or `InternNav-ros2-client`, as both depend on this package.

## License

This project is licensed under the Apache 2.0 License. See [LICENSE](LICENSE) for details.
