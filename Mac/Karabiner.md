# Karabiner

## 1. 下载

自己搜教程吧

## 2. 进入配置文件目录

主页-Misc-open config folder

进入assets/complex_modificaations

写入json文件

```json
{
  "title": "caps to Hyper When Held",
  "rules": [
    {
        "description": "CAPS LOCK + hjklio to arrow keys",
        "manipulators": [
            {
              "conditions": [
                  {
                      "name": "caps_lock pressed",
                      "type": "variable_if",
                      "value": 1
                  }
              ],
              "from": {
                  "key_code": "i",
                  "modifiers": {
                      "optional": [
                          "any"
                      ]
                  }
              },
              "to": [
                  {
                      "key_code": "home"
                  }
              ],
              "type": "basic"
            },
            {
            "conditions": [
                {
                    "name": "caps_lock pressed",
                    "type": "variable_if",
                    "value": 1
                }
            ],
            "from": {
                "key_code": "o",
                "modifiers": {
                    "optional": [
                        "any"
                    ]
                }
            },
            "to": [
                {
                    "key_code": "end"
                }
            ],
            "type": "basic"
            },
            {
                "conditions": [
                    {
                        "name": "caps_lock pressed",
                        "type": "variable_if",
                        "value": 1
                    }
                ],
                "from": {
                    "key_code": "j",
                    "modifiers": {
                        "optional": [
                            "any"
                        ]
                    }
                },
                "to": [
                    {
                        "key_code": "down_arrow"
                    }
                ],
                "type": "basic"
            },
            {
                "conditions": [
                    {
                        "name": "caps_lock pressed",
                        "type": "variable_if",
                        "value": 1
                    }
                ],
                "from": {
                    "key_code": "k",
                    "modifiers": {
                        "optional": [
                            "any"
                        ]
                    }
                },
                "to": [
                    {
                        "key_code": "up_arrow"
                    }
                ],
                "type": "basic"
            },
            {
                "conditions": [
                    {
                        "name": "caps_lock pressed",
                        "type": "variable_if",
                        "value": 1
                    }
                ],
                "from": {
                    "key_code": "h",
                    "modifiers": {
                        "optional": [
                            "any"
                        ]
                    }
                },
                "to": [
                    {
                        "key_code": "left_arrow"
                    }
                ],
                "type": "basic"
            },
            {
                "conditions": [
                    {
                        "name": "caps_lock pressed",
                        "type": "variable_if",
                        "value": 1
                    }
                ],
                "from": {
                    "key_code": "l",
                    "modifiers": {
                        "optional": [
                            "any"
                        ]
                    }
                },
                "to": [
                    {
                        "key_code": "right_arrow"
                    }
                ],
                "type": "basic"
            },
            {
                "from": {
                    "key_code": "caps_lock",
                    "modifiers": {
                        "optional": [
                            "any"
                        ]
                    }
                },
                "to": [
                    {
                        "set_variable": {
                            "name": "caps_lock pressed",
                            "value": 1
                        }
                    }
                ],
                "to_after_key_up": [
                    {
                        "set_variable": {
                            "name": "caps_lock pressed",
                            "value": 0
                        }
                    }
                ],
                "to_if_alone": [
                    {
                        "hold_down_milliseconds": 100,
                        "key_code": "escape"
                    }
                ],
                "type": "basic"
            }
        ]
    }
]
}
```

实现的是按住为方向键

点按为esc 时间为100ms

因此shift不影响esc使用 保持原有习惯