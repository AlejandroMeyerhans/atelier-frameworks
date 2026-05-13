# Audience Avatars

This directory holds psychographic avatar files used to calibrate voice output for specific audiences.

## How It Works

When you run the `adjusting-voice` skill, it checks this directory for avatar files. If it finds any, it lists them and lets you choose which audience to target. The voice stays the same — the *calibration* shifts to match the audience's pain points, vocabulary, trust triggers, and expertise level.

## Creating Avatar Files

Use the `defining-avatars` skill from this same repo ([atelier-frameworks](https://github.com/AlejandroMeyerhans/atelier-frameworks)). It produces deep psychographic dossiers through a progressive discovery interview.

Place the output here with a descriptive filename:
- `marketing-martha.md`
- `ecommerce-eric.md`
- `agency-owner.md`
- `startup-founder.md`

## Without Avatars

The skill works without avatar files — it applies the voice generically. You can also describe the target audience verbally during a run, though avatar files provide significantly richer calibration.
