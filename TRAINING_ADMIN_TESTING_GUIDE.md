# CTrack Beta Testing Guide - Training Admin Permissions

## Overview
This guide covers functionality available to users with **Training Admin permissions** in CTrack. Training Admins can manage day-to-day training operations but have limited access to server configuration compared to full Admins.

## Prerequisites
- **Role Required**: Training Admin role configured in the guild settings
- **Permissions**: Training administration privileges (not server owner)
- **Access Level**: Training management, student administration, reporting

---

## Phase 1: Student Management & Training Operations

### 1.1 Student Status & Waitlist Management
**Commands**: `/admin student` group commands
**Steps**:

#### Status Management:
1. Test `/admin student set-status` with various students:
   - Set waitlist statuses: `Standby`, `Hold (Academy)`, `Hold (Hours)`, `Hold (Validation)`, `Hold (Admin) Contact TA`
   - Verify you can manage students on multiple waitlists
   - Test setting overall status (Active/Inactive) for non-waitlist students
2. Use `/admin student inactive` and `/admin student archive`:
   - Test both with and without `silent: true` option
   - Verify proper DM notifications sent
   - Confirm waitlist removal

#### Waitlist Operations:
1. Test `/admin student add-to-waitlist`:
   - Add students to Primary waitlist
   - Add students to Specialized waitlist (if enabled)
   - Verify proper training type selection modal
2. Use `/admin student set-waitlist-date`:
   - Modify waitlist entry dates using YYYY-MM-DD format
   - Verify waitlist order updates correctly

### 1.2 Assignment Management
**Commands**: `/admin assign-student`, `/admin remove-student`
**Prerequisites**: Active students on waitlist, available instructors
**Steps**:

#### Student Assignment:
1. Assign students from Primary waitlist to instructors
2. Assign students from Specialized waitlist to instructors
3. Test multi-waitlist scenarios (should prompt for type selection)
4. Verify assignment notifications sent properly
5. Confirm students removed from appropriate waitlist only

#### Assignment Removal:
1. Remove assignments in various states (Pending, Accepted)
2. Verify students restored to correct waitlist type
3. Check instructor channel access removed
4. Confirm notification messages sent to both parties

### 1.3 Student Notes & Documentation
**Commands**: `/admin student manage-waitlist-notes`, `/admin student manage-ots-notes`
**Steps**:
1. Add, edit, and remove notes for students on waitlist
2. Test note management for students on multiple waitlists
3. Manage notes for students on OTS waitlist
4. Verify note updates appear in waitlist embeds

### 1.4 Student Records Review
**Command**: `/admin student view-inactive-archived`
**Steps**:
1. Generate report of inactive students
2. Generate report of archived students
3. Review comprehensive formatting and data accuracy

---

## Phase 2: Assignment & Instructor Management

### 2.1 Instructor Capacity Management
**Command**: `/admin set-max-students`
**Prerequisites**: Users with instructor/mentor roles
**Steps**:
1. Modify maximum student capacity for instructors (range 1-10)
2. Test with various instructor types (instructor vs mentor)
3. Verify capacity reflected in instructor dashboards
4. Attempt to set capacity for non-instructors (should error)
5. Confirm embed updates after changes

---

## Phase 3: OTS (Over-the-Shoulder) Administration

### 3.1 OTS Workflow Management
**Commands**: `/admin student ots-return`, `/admin student ots-cancel`
**Prerequisites**: Students with active OTS sessions
**Steps**:

#### OTS Returns:
1. Return OTS student to waitlist (incomplete evaluation)
2. Verify student status updated to 'Hold (Hours)'
3. Confirm student appears on OTS waitlist embed
4. Check proper notifications sent

#### OTS Cancellations:
1. Cancel OTS nomination entirely
2. Verify student returned to original instructor
3. Confirm assignment notification sent for re-acceptance
4. Check OTS waitlist updated correctly

---

## Phase 4: Training System Configuration

### 4.1 Specialized Training Management
**Commands**: `/admin training-types add`, `/admin training-types list`, `/admin training-types remove`
**Prerequisites**: Special training enabled in configuration
**Steps**:
1. Add new specialized training types:
   - Use descriptive names (e.g., "Ground Radar", "TRACON Approach")
   - Verify no duplicate names allowed
2. List all configured training types with IDs
3. Remove training types via selection menu
4. Test waitlist functionality with new types

### 4.2 Form System Management
**Commands**: `/admin form create`, `/admin form remove`
**Steps**:

#### Form Creation:
1. Create Student forms:
   ```json
   [{"question": "What is your current rating?", "required": true}, {"question": "Describe your training goals", "required": false}]
   ```
2. Create Instructor forms:
   ```json
   [{"question": "What type of training request?", "required": true}, {"question": "Additional details", "required": false}]
   ```
3. Verify forms appear in forms channel embed

#### Form Management:
1. Remove forms using selection menu
2. Verify form submissions still accessible after form removal
3. Test with multiple forms of each type

---

## Phase 5: Comprehensive Reporting

### 5.1 Student & Training Reports
**Commands**: Various `/admin reports` commands
**Steps**:

#### Individual Reports:
1. Generate user reports (`/admin reports user`):
   - Test with Discord mentions (@user)
   - Test with VATSIM CIDs (numerical)
   - Test with Discord IDs
   - Verify comprehensive data display

#### Waitlist Analysis:
1. Generate current waitlist report (`/admin reports waitlist`)
2. Filter waitlist by rating (`/admin reports waitlist S1`)
3. Verify position calculations and status accuracy

#### Specialized Reports:
1. OBS student report (`/admin reports obs`):
   - Export to text file
   - Verify inactive student identification
2. Instructor performance report (`/admin reports ins`):
   - Review capacity utilization
   - Check activity metrics
   - Verify color-coded status indicators

#### Activity Reports:
1. Group session statistics (`/admin reports group-sessions`):
   - Default 30-day period
   - Custom time periods (test with 7, 60, 90 days)
   - Verify attendance calculations

#### Progress Tracking:
1. Individual progress reports (`/admin reports progress <user> <rating>`):
   - Test with various VATSIM users
   - Verify hours data retrieval
   - Check requirement comparisons

### 5.2 Form Submission Management
**Commands**: `/admin reports req`, `/admin reports req-all`
**Prerequisites**: Submitted forms in the system
**Steps**:
1. View all form submissions (`/admin reports req-all`)
2. Filter submissions by specific user
3. View detailed submission (`/admin reports req <id>`)
4. Use action buttons to approve/deny submissions
5. Add admin comments to submissions
6. Verify status updates and notifications

### 5.3 Report Documentation
**Command**: `/admin reports help`
**Steps**:
1. Review comprehensive report documentation
2. Verify all report types listed with descriptions
3. Check usage examples and pro tips

---

## Phase 6: Team Communication Management

### 6.1 Notice Board Administration
**Commands**: `/admin notice new`, `/admin notice manage`
**Steps**:

#### Notice Creation:
1. Create notices with expiration dates:
   - Test various expiration periods (days)
   - Create permanent notices (no expiration)
2. Verify notice content formatting and display

#### Notice Management:
1. Manage existing notices (`/admin notice manage <id>`):
   - View notice details and review status
   - Edit notice content
   - Change expiration dates
   - Delete notices
2. Verify notice board embed updates after changes

---

## Phase 7: System Maintenance & Configuration

### 7.1 Embed Management
**Commands**: `/admin config refresh-embeds`, `/admin channel-recovery`
**Steps**:
1. Manually refresh all embeds in server
2. Verify all dynamic content updates properly
3. Test embed recovery for missing/corrupted embeds
4. Confirm instructor dashboards update correctly

### 7.2 Configurable Messages
**Command**: `/admin config set-message`
**Message Types**: `inactive_dm`, `archive_dm`, `training_policy`
**Steps**:
1. Customize inactive student DM message
2. Set custom archive notification message
3. Update training policy message content
4. Verify messages used in relevant operations
5. Test training policy embed updates

### 7.3 Progress Requirements Configuration
**Commands**: `/admin config set-progress-requirements`, `/admin config view-progress-requirements`
**Prerequisites**: Valid ARTCC configuration
**Steps**:

#### Requirement Setup:
1. Configure S1 rating requirements:
   - Set training hours (e.g., 10 hours)
   - Define training positions (e.g., "ABQ_TWR", "PHX_GND")
   - Set OTS hours (e.g., 15 hours)
   - Define OTS positions (e.g., "ABQ_APP", "PHX_APP")
2. Configure additional ratings (S2, S3, C1)
3. Test interactive setup interface

#### Requirement Management:
1. View all configured requirements
2. Verify position lists and hour requirements
3. Test with progress report generation

---

## Phase 8: Data Validation & Error Handling

### 8.1 Input Validation
**Steps**:
1. Test commands with invalid user identifiers
2. Attempt operations on non-existent students
3. Test with invalid date formats for waitlist dates
4. Verify proper error messages for all scenarios

### 8.2 Permission Boundaries
**Steps**:
1. Verify access to training administration commands
2. Confirm no access to server initialization (`/admin init`)
3. Test boundaries with developer commands (`/dev` - should be restricted)
4. Validate proper error messages for restricted commands

### 8.3 Data Consistency
**Steps**:
1. Verify database updates reflected across all embeds
2. Test concurrent operations (multiple admins working simultaneously)
3. Check assignment state consistency across operations
4. Validate waitlist position calculations after modifications

---

## Expected Behaviors & Validation Points

### Success Indicators:
- All training admin commands execute successfully
- Proper confirmation messages for all operations
- Student data updates consistently across system
- Reports generate accurate, current information
- Form system operates smoothly end-to-end
- Notice board updates reflect changes immediately

### Key Validations:
- ✅ Student progression managed effectively
- ✅ Assignment workflow operates correctly
- ✅ OTS system functions as designed
- ✅ Reporting provides actionable insights
- ✅ Form submissions managed properly
- ✅ Notice board facilitates team communication
- ✅ Progress tracking supports student development

### Critical Issues to Report:
- Commands failing with system errors
- Missing or incorrect notifications
- Data inconsistencies between views
- Report generation failures
- Form system malfunctions
- Embed update failures
- Permission escalation issues

---

## Scope Limitations

**Training Admins should NOT have access to**:
- Server initialization (`/admin init`)
- Core server configuration changes
- Developer commands (`/dev` group)
- Role mapping modifications

**Training Admins SHOULD have access to**:
- All student management operations
- Assignment and instructor management
- OTS administration
- Comprehensive reporting
- Form system management
- Notice board administration
- Training-specific configuration

---

## Post-Testing Checklist

After completing all tests:
- [ ] Student management workflow functional
- [ ] Assignment system operates correctly
- [ ] OTS workflow complete and accurate
- [ ] All reports generate successfully
- [ ] Form submissions manageable
- [ ] Notice board updates properly
- [ ] Progress tracking accurate
- [ ] Specialized training system functional
- [ ] Instructor capacity management works
- [ ] Proper permission boundaries maintained
- [ ] Error handling appropriate for all scenarios
- [ ] Database consistency maintained across operations