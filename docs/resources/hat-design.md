# Design of the Robots10x Pi HAT+

To facilitate 

## Design Specification

The https://pip-assets.raspberrypi.com/categories/1215-raspberry-pi-hat/documents/RP-008281-DS-1-hat-plus-specification.pdf

### Requirements

design guide: https://github.com/raspberrypi/hats/blob/master/designguide.md

ideal diode from spec: https://github.com/raspberrypi/hats/blob/master/zvd-circuit.png

ptc fuses: https://www.digikey.com.au/en/products/filter/ptc-resettable-fuses/150?s=N4IgjCBcoGwBwCYqgA4BcogKoDsCWaA8gGYCyApgIYDOArgE7kgA0ItmAgiyALZ46YArCAC%2BrALRJoIAMZQ09WuVYB7KAG0Qw1gE4QAXTEhxe6XMgKlqjeAMj7QA
atm fuses: https://www.digikey.com.au/en/products/filter/fuses/139?s=N4IgjCBcoCwJxVAYygMwIYBsDOBTANCAPZQDaIAzGAGxxgBMIAuoQA4AuUIAyuwE4BLAHYBzEAF9C9AAwAOWYhAcuAVSED2AeVQBZXOmwBXPrhCFDXAIJmQAW2FcArDdvoAHlzDSJkkNUUCACZcALReEGyckCA2AI7sAJ5ONomsptEGKOLiQA
vtg regs: https://www.digikey.com.au/en/products/filter/power-management-pmic/voltage-regulators-dc-dc-switching-regulators/739?s=N4IgjCBcpgTAnFUBjKAzAhgGwM4FMAaEAeygG0RYAWAdhoAYA2EI6ugZnZcqoA45ErPmBrMhvWOzE8JVKt0lxJC9ot4rYvRjQ28GCxo1iMIrQ5p1nG7GqcqH28WAcZUwAVgXuPYea29OnkTmrtKw7ghGXpFBlO5y4Qq89AzqZvDJsbAMVPRplDlwCvA21MU27H6UJVr5mo6V3Oz0fPCCIM1U8C3FNKp2NNRu3IO0zkR9YNYjGdrctcbzsC2xvCXwVfCGJtxg9OFgdryV-Pl7onzc2zS0u3BTdoewU9KH7ry8VW8bj2A-XBN6DYwGcqMsuvM8qddlQjIcYWtpkQfO4bLt4lQ0cj3lIAeB3nJXtYPONwMcuniQex3qS-uwJPQFL5HFVJHRMV5DPCALpEAAOABcoCAAMoCgBOAEsAHYAcxAAF9kfQMkgQKhIJhcIQSOQOpITJZ9VIIk0DcszVJspajPlVFbELyQILhWKpXLFUQALTOaDqqASgCuOtIkAo7U83KVIC9iD9GqDIb1ECj0eYfslABNhV69nYXZAQNwAI4CgCewti5b5eGFGBwqAVCqAA
fuse holders: https://www.digikey.com.au/en/products/filter/fuseholders/140?s=N4IgjCBcoCwOxVAYygMwIYBsDOBTANCAPZQDaIMArAAwDMAHAJwgC6hADgC5QgDKnAJwCWAOwDmIAL6EAbM2ggUkDDgLEyFMGCYJCMao1qHWHbpD6DREydJAAmDQCNM6ACa4ABKgCueDwAsiTHcBExAZRBAhVx4AWjBqCFMeEEIAR04ATx5KVJAs9lwedGwUGyA

chosen reg?: TPS566247DRLR
design guide: https://www.youtube.com/watch?v=IyiCHMHE5Qg

- Fuse: Either PTC fuse (5A? unlikely) or mini automotive blade fuse like currently (ATM fuse)
- Power:
  - Low batt vtg LED
  - Fuse blown indicator?
  - Ideally batt ADC measurement
  - RVP
  - Pi back-power prevention
- I/O:
  - Motor driver connections
  - Ultrasonic sensor
  - Buttons?
  - Servo?
  - Qwiic?

## 

Either a Power HAT+ or Standard  (or non-compliant? and just set firmware max usb current option)
It is a Power HAT+, as it powers the Raspberry Pi by providing 5.1V at 5A to the GPIO pins: AKA class 11.
This means it *should* have an EEPROM addressed 

Requires 5.1V at 3A (minimum) or (pref.) 5A on GPIO, capable of handling 3V3 present or not, and back-powering from USB

BK-1603 mini blade (aka ATM) fuse holder

