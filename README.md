# Sensor Watch

Tell it once what normal looks like, for every sensor in the house, and it tells you only when something isn't: what needs doing, or has gone wrong, before the family notices.

> **Maturity: Beta.** Complete and used every day; its features have settled. Please report what breaks in your setup. ([The levels](https://github.com/gazoodle/casa-mia/blob/2026.11.5/docs/README.md#maturity))

<img src="https://raw.githubusercontent.com/gazoodle/casa-mia/2026.11.5/docs/screenshots/sensor-watch-card.webp" alt="A Home Assistant dashboard view named Sensor Watch. On the left the Sensor Watch card lists what needs attention, worst first: an error (Boiler fault, problem reported), a warning (Hall smoke alarm battery, battery flat, 4%) and four tasks (three updates available, and a front door sensor battery to replace at 17%), each with its level as a coloured pill, its message, its value and how long it has stood. On the right four Sensor Watch gauges, each an arc of its watch's coloured bands with a needle: mains voltage 241 V, nominal; hot water 46.8 °C, nominal; the hall smoke alarm at 4%, warning, battery flat; and the landing smoke alarm at 88%, nominal" width="800">

## What it's for

Home Assistant is great when it's all working. When it isn't, it's a pain, and only then
do you discover the things that have been in error for ages: a sensor unavailable since
the spring, an integration that never came back after an update, a battery long flat.

Has anyone else looked at 30 Hue bulbs and 20 Shelly switches and decided not to bother
with an automation for each one dropping out of range? Or built a dashboard panel for
the things that need attention, knowing all the while that something was missed? Sensor
Watch is for that. Tell it once what normal looks like, sensor by sensor or with a scan
of the whole house (it suggests the bands from history, and knows what a leak sensor or
a low battery means without being told), and it keeps watching, Home Assistant itself
included: its Recorder, and every integration that fails to set up.

It isn't a replacement for automations: it's a grown-up notification system that you
configure once. Automations are for taking action; Sensor Watch is the trigger that
starts them. On each change of level it fires an event, and its status, counts and List
action always say what's wrong, so you choose what happens next:

- **Tell someone:** a notification when anything becomes a task, a warning to the phone
  of whoever's home, critical to everyone. The **Notify on Sensor Watch** blueprint does
  this in a few clicks ([The event](https://github.com/gazoodle/casa-mia/blob/2026.11.5/docs/applets/sensor-watch.md#the-event)).
- **Show it:** a panel of what needs attention on the wall tablets. Pair it with
  [garnish](https://github.com/gazoodle/casa-mia/blob/2026.11.5/docs/tablet-layout.md#showing-and-hiding), so the panel's heading
  disappears with it on a quiet day, rather than a proud *WARNINGS* over nothing.
- **Look into it:** hand the list to an AI agent (Home Assistant's AI tasks, say) to
  investigate what has gone wrong and why, before you even reach for the laptop.
- **Keep a to-do list for the house:** each task (top up the salt a [Salt Sentry][salt-sentry]
  measures, change a battery, a
  filter due) added to a Home Assistant to-do list, and ticked off by itself when the
  sensor is nominal again.
- **Escalate:** a warning nobody has dealt with in a day becomes a text, through
  [Phone and SMS](https://github.com/gazoodle/casa-mia/blob/2026.11.5/docs/applets/phone-and-sms.md), which works even when the internet doesn't.
- **Say it with a light:** the hallway lamp glows amber while anything is a warning.
- **Put it over everything:** a critical comes up on every wall tablet, over whatever
  it's showing, with the [Over layer](https://github.com/gazoodle/casa-mia/blob/2026.11.5/docs/over-layer.md).
- **Brief the morning:** the voice assistant reads out the day's tasks at breakfast.
- **Watch the trends:** the counts are measurements, so Home Assistant's own history
  shows which integration falls over most often, and when.

Each sensor gets a level:

| Level | Means | Example |
|---|---|---|
| **Nominal** | All is well. | The softener's salt is above 25%. |
| **Task** | Something to do, not a fault. | Top up the salt. |
| **Warning** | Worth a look. | The freezer is at −14 °C. |
| **Error** | Something is wrong. | The freezer is at −8 °C, or its sensor is unavailable. |
| **Critical** | Drop everything. | A leak sensor is wet. |

A sensor that goes **unavailable** is part of this, not an afterthought: by default it
counts as an error, because a sensor that has stopped reporting is often the first sign
of a broken integration or a flat battery. It counts only once it has been unavailable for
five minutes (yours to change), as a restart, a reload or a car asleep is usual, not
trouble.

[salt-sentry]: https://www.tindie.com/products/ErikLemcke/salt-sentry-water-softener-monitor/

## Installing

Sensor Watch needs Home Assistant 2026.3.0 or later.

1. In HACS, or in Home Assistant's Marketplace (2026.11 and later), add
   `https://github.com/gazoodle/casa-mia-sensor-watch` as a custom repository of the type Integration.
2. Download Sensor Watch there, then restart Home Assistant.
3. In Settings → Devices & services, choose Add integration and pick Sensor Watch.

The [guide](https://github.com/gazoodle/casa-mia/blob/2026.11.5/docs/applets/sensor-watch.md) covers setting it up and everything on its page.

## Part of Casa Mia

Sensor Watch is part of [Casa Mia](https://github.com/gazoodle/casa-mia), where it is written and
released. This repository is generated from Casa Mia 2026.11.5 (commit `e9c01779a2`) and
isn't edited by hand, so [issues](https://github.com/gazoodle/casa-mia/issues) and changes go to Casa Mia.

The Casa Mia app installs this same integration itself. A house with both needs to do
nothing about it: [With HACS or the Marketplace](https://github.com/gazoodle/casa-mia/blob/2026.11.5/docs/applets/sensor-watch.md#with-hacs-or-the-marketplace)
says what happens.
