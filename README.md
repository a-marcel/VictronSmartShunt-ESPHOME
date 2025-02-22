# VictronSmartShunt-ESPHOME
ESPHome component to monitor a Victron BMV and SmartShunt via ve.direct / UART TTL

## Supported devices

All BMV and SmartShunt providing a ve.direct port.

## Tested devices

  * Victron SmartShunt 500A/50mV


## Requirements

* [ESPHome 2021.10 or higher](https://github.com/esphome/esphome/releases).
* Generic ESP32 or ESP8266 board

## Schematics

```
                UART-TTL
┌────────────────┐                ┌──────────────────┐
│           GND o│<-------------->│o GND             │
│ BMV or     TX o│--------------->│o D7   ESP32/     │
│ SmartShunt RX o│                │       ESP8266    │<-- GND
│       5V/3.3V o│                │                  │<-- 3.3V
└────────────────┘                └──────────────────┘

# UART-TTL jack (JST-PH 2.0mm pinch)
┌─── ─────── ────┐
│                │
│ O   O   O   O  │
│GND  RX  TX VCC │
└────────────────┘
```

If you are unsure about to pin order please measure the voltage between GND and VCC (5V/3.3V). If you measure a positive voltage you know the position of VCC and GND!

### JST-PH jack

| Pin     | Purpose      | ESP pin        |
| :-----: | :----------- | :------------- |
|  **1**  | **GND**      | GND            |
|    2    | RX           |                |
|  **3**  | **TX**       | D7 (RX)        |
|    4    | 5V           |                |

## Installation

You can install this component with [ESPHome external components feature](https://esphome.io/components/external_components.html) like this:

Example:
```yaml
external_components:
  - source: github://KinDR007/VictronSmartShunt-ESPHOME@main

victron_smart_shunt:
  uart_id: the_uart

sensor:
  - platform: victron_smart_shunt
    battery_voltage:
      id: bv
    battery_current:
      id: bc
```

The `uart_id` is optional.

All sensors are optional.

```yaml
  - platform: victron_smart_shunt
    battery_voltage:
      name: "Battery Voltage"  
      id: bv

    battery_current:
      name: "Battery Current" 
      id: bc

    fw_version:
      name: "fw"  
      id: fw

    pid:
      name: "pid"  
      id: pid

    instantaneous_power:
      name: "instantaneous power"  
      id: instantaneous_power      

    time_to_go:
      name: "time to go"  
      id: time_to_go

    consumed_amp_hours:
      name: "consumed amp hours"
      id: consumed_amp_hours  
      unit_of_measurement: Ah

    min_battery_voltage:
      name: "Min battery voltage"
      id: min_battery_voltage   

    max_battery_voltage: 
      name: "Max battery voltage"
      id: max_battery_voltage     

    amount_of_charged:
      name: "Amount of charged"
      id:  amount_of_charged   
      filters:
        - multiply: 0.001
      unit_of_measurement: kWh

    bmv_alarm:
      name: "BMV alarm"
      id: bmv_alarm
      
    bmv_pid:
      name: "bmv - pid"
      id: bmv_pid

    last_full_charge:
      name: "Time since last full charge"
      id: last_full_charge

    deepest_discharge:
      name: "Depth of the deepest discharge"
      id: deepest_discharge   
      unit_of_measurement: Ah

    last_discharge:
      name: "Depth of the last discharge"
      id: last_discharge
      unit_of_measurement: Ah

    discharged_energy:
      name: "Amount of discharged energy"
      id: discharged_energy   
      filters:
        - multiply: 0.001
      unit_of_measurement: kWh

    state_of_charge:
      id: state_of_charge
      name: "SoC"  
```
The available numeric sensors are:
- `instanteneous_power`
- `time_to_go`
- `state_of_charge`
- `consumed_amp_hours`
- `min_battery_voltage`
- `max_battery_voltage`
- `amount_of_charged`
- `last_full_charge`
- `deepest_discharge`
- `last_discharge`
- `discharged_energy`
- `number_of_full_dis`
- `number_of_charge_cycles`


The available text sensors are:
- `bmv_alarm_text`
- `bmv_text`
- `charger_text`
- `error_text`
- `alarm_reason_text`
- `tracker_text`
- `fw_version`
- `pid`



Full example in `smartshunt.yaml`

`Big thanks for help to ssieb`

```
#victron #esphome #smartshunt #bmv #ve.direct 
