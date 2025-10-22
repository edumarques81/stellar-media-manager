# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a photography management system being developed to replace existing software (Netlife and Skill Chair) for a photography business that operates in three main areas:

1. **Youth Sports Photography**: Action shots of children in local sports clubs
2. **School Portraits**: Graduation photos, dances, school events
3. **Event Coverage**: Rugby tournaments, Lusatra, and various events

### Business Model
- Photos are sold to parents through an online store
- Photos organized by teams with individual child identification
- Uses facial recognition AI and jersey number recognition
- Parents access photos via unique codes

### Key Requirements
- **Privacy & Security**: Handling sensitive data about children (PII) with parental consent
- **No QR/Barcode Systems**: Considered confusing and error-prone
- **Competitive Advantage**: Custom features not available to competitors
- **Future Goal**: License the software to third parties and eventually sell the business

## Project Status

**Currently in design phase** - only documentation exists so far. The codebase will be built to integrate with Timestone software while providing custom functionality.

## Project Documentation

### Design Documents Location
All design and specification documents are in [project-design/](project-design/)

### Key Design Document
[project-design/first_meeting_summary-pt.md](project-design/first_meeting_summary-pt.md) (in Portuguese) contains the comprehensive meeting notes including:
- Current systems and workflows
- Problems with current software
- Future objectives and next steps
- Security and privacy considerations
- Data structures and booking modules

## Architecture Considerations (When Implementation Begins)

### Core System Requirements
1. **Booking Module**: Clubs request photographers, submit player data via portal
2. **Player/Team Management**: Organize by season/year, handle team changes, absences, sibling photos
3. **Photo Organization**: Group by club → teams (by age) → individuals
4. **Online Store Integration**: Full e-commerce functionality
5. **Image Upload/Storage**: Local editing → Australian server upload with semi-annual backup to external HD
6. **Recognition Systems**:
   - Facial recognition AI
   - Jersey/number recognition for sports events
7. **Access Control**: Unique codes for parents to download photos

### Integration Points
- **Timestone Software**: Primary system to integrate with - requires API research
- **Data Import**: Handle spreadsheet imports from clubs/schools (name, age, team, parent contact info)
- **Storage**: Australian server architecture for production images

### Data Privacy & Security
- Children's personal identifiable information (PII)
- Parental consent management
- Marketing consent toggles
- Secure access codes for photo downloads

## Development Workflow (To Be Established)

When the implementation phase begins, this section will be updated with:
- Technology stack decisions
- Build commands
- Test commands
- Deployment procedures
- Development environment setup

## Contact & Decision Making

Project owner: Eduardo Marques (eduardo.marquesmarques81@gmail.com)

Note: Business partner currently on vacation - no immediate urgency for development timeline.
