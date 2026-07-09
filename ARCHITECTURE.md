# IEXEL Club OS Architecture

## Purpose

IEXEL Club OS is a modular WordPress-based football club operating system.

It is designed to support grassroots clubs first, while remaining scalable for academies, semi-professional clubs and professional organisations.

## Core Principles

- Modular features
- Clean separation of responsibilities
- Reusable components
- Configurable club settings
- Feature toggles for advanced functionality
- Repository-based database access
- Page classes for admin UI screens
- One source of truth for club data

## Current Modules

### Core
- DatabaseManager
- SettingsManager
- ModuleManager
- ActivityLogger
- AdminUI

### People
Handles members, players, coaches, parents, volunteers and staff.

### Teams
Handles teams, age groups, formats and team profiles.

### Team Assignments
Links people to teams with roles such as player, coach, parent and volunteer.

## Development Rules

- One feature per branch
- Commit after each stable milestone
- Pull request into main only when tested
- Avoid adding new large methods to AdminUI.php
- Move reusable UI into Components
- Move full pages into Pages
- Keep database operations inside repository classes
- Use SettingsManager for configurable behaviour
