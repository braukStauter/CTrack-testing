# CTrack Beta Testing Guide - Admin Permissions

## Overview
This guide covers all functionality available to users with **Admin permissions** in CTrack. Admin users have the highest level of access and can manage all aspects of the training system.

## Prerequisites
- **Role Required**: Admin role configured in the guild settings
- **Permissions**: Server administrator or designated admin role
- **Access Level**: Full system access including server initialization

---

## Phase 1: Initial Setup & Configuration

### 1.2 Configuration Management
**Commands**: Various `/admin config` commands
**Steps**:
1. Test `/admin config refresh-embeds` - verify all embeds update
2. Test `/admin config set-message` for each message type:
   - `inactive_dm`
   - `archive_dm`
   - `training_policy`
3. Verify training policy embed updates when setting training_policy message

---

## Phase 2: User & Student Management

### 2.1 Student Status Management
**Commands**: `/admin student set-status`, `/admin student inactive`, `/admin student archive`
**Test Users**: Use existing members or create test accounts
**Steps**:

#### Status Setting Tests:
1. Test setting overall statuses (Active/Inactive) for users NOT on waitlist
2. Test setting waitlist statuses for users ON waitlist:
   - `Standby`
   - `Hold (Academy)`
   - `Hold (Hours)`
   - `Hold (Validation)`
   - `Hold (Admin) Contact TA`
3. Verify error handling when trying to set Active/Inactive for waitlist users
4. Test with users on multiple waitlists (should prompt for selection)

#### Inactive/Archive Tests:
1. Use `/admin student inactive` on active student
2. Verify student removed from waitlist and status set to Inactive
3. Test with `silent: True` option
4. Repeat for `/admin student archive`

### 2.2 Waitlist Management
**Commands**: `/admin student add-to-waitlist`, `/admin student set-waitlist-date`
**Steps**:
1. Manually add student to Primary waitlist
2. Manually add student to Specialized waitlist (if enabled)
3. Attempt to add same student to same waitlist type (should error)
4. Test date modification with `/admin student set-waitlist-date`
   - Use format YYYY-MM-DD
   - Verify waitlist order updates correctly

### 2.3 Assignment Management
**Commands**: `/admin assign-student`, `/admin remove-student`
**Prerequisites**: Students on waitlist, available instructors
**Steps**:

#### Assignment Tests:
1. Assign student from Primary waitlist to instructor
2. Assign student from Specialized waitlist to instructor
3. Test assignment of student on multiple waitlists (should prompt for type selection)
4. Verify assignment notification sent to student
5. Verify student removed from appropriate waitlist
6. Test assignment of already-assigned student (should error)

#### Removal Tests:
1. Remove assignment before student accepts
2. Remove assignment after student accepts
3. Verify student restored to correct waitlist type
4. Verify student removed from instructor channel access
5. Check notifications sent to both parties

### 2.4 Student Records & Reports
**Commands**: `/admin student view-inactive-archived`, `/admin student manage-waitlist-notes`, `/admin student manage-ots-notes`
**Steps**:
1. View list of inactive/archived students
2. Add/edit/remove notes for students on waitlist
3. Test note management for students on multiple waitlists
4. Manage OTS waitlist notes for nominated students

---

## Phase 3: Instructor & Capacity Management

### 3.1 Instructor Capacity
**Command**: `/admin set-max-students`
**Prerequisites**: Users with instructor/mentor roles
**Steps**:
1. Set max student capacity for various instructors (range 1-10)
2. Verify capacity updates reflected in instructor dashboard
3. Test setting capacity for non-instructor (should error)
4. Verify embed updates after capacity changes

---

## Phase 4: Training System Management

### 4.1 Specialized Training Types
**Commands**: `/admin training-types add`, `/admin training-types list`, `/admin training-types remove`
**Prerequisites**: Special training enabled in guild config
**Steps**:
1. Add new specialized training type (e.g., "Ground Radar")
2. List all training types
3. Remove a training type
4. Verify waitlist functionality with specialized types

### 4.2 Form Management
**Commands**: `/admin form create`, `/admin form remove`
**Steps**:
1. Create Student form with sample questions:
   ```json
   [{"question": "What is your current rating?", "required": true}]
   ```
2. Create Instructor form with multiple questions
3. Test form removal via selection menu
4. Verify forms appear in forms channel embed

### 4.3 Progress Requirements
**Commands**: `/admin config set-progress-requirements`, `/admin config view-progress-requirements`
**Prerequisites**: Valid ARTCC configuration
**Steps**:
1. Configure progress requirements for S1 rating:
   - Set training hours requirement
   - Add qualifying positions (e.g., "ABQ_TWR", "PHX_GND")
   - Set OTS hours requirement
   - Add OTS qualifying positions
2. Configure requirements for additional ratings (S2, S3, C1)
3. View configured requirements
4. Test progress reports with `/admin reports progress`

---

## Phase 5: OTS (Over-the-Shoulder) Management

### 5.1 OTS Operations
**Commands**: `/admin student ots-return`, `/admin student ots-cancel`
**Prerequisites**: Students with claimed OTS sessions
**Steps**:
1. Return OTS student to waitlist (simulates incomplete OTS)
2. Cancel OTS nomination entirely (returns to original instructor)
3. Verify proper status updates and notifications
4. Check OTS waitlist embed updates

---

## Phase 6: Team Communication

### 6.1 Notice Board Management
**Commands**: `/admin notice new`, `/admin notice manage`
**Steps**:
1. Create new team notice with expiration
2. Create permanent notice (no expiration)
3. Use `/admin notice manage` with notice ID to:
   - View notice details
   - Edit notice content
   - Change expiration
   - Delete notice
4. Verify notice board embed updates

---

## Phase 7: Reporting & Analytics

### 7.1 Comprehensive Reports
**Commands**: Various `/admin reports` commands
**Steps**:

#### User Reports:
1. `/admin reports user` with Discord mention
2. `/admin reports user` with VATSIM CID
3. `/admin reports user` with Discord ID

#### Request Management:
1. `/admin reports req-all` - view all form submissions
2. `/admin reports req <id>` - view specific submission
3. Use action buttons to approve/deny requests

#### Specialized Reports:
1. `/admin reports obs` - generate OBS student report
2. `/admin reports ins` - comprehensive instructor report
3. `/admin reports waitlist` - current waitlist analysis
4. `/admin reports waitlist <rating>` - filtered by rating
5. `/admin reports group-sessions` - group session statistics
6. `/admin reports progress <user> <rating>` - individual progress

#### Report Help:
1. `/admin reports help` - view all available reports

---

## Phase 8: System Maintenance

### 8.1 Channel & Embed Recovery
**Commands**: `/admin channel-recovery`
**Steps**:
1. Manually delete a dynamic embed from a channel
2. Run `/admin channel-recovery`
3. Verify missing embeds are recreated
4. Check that all embeds are properly formatted

### 8.2 Configurable Messages
**Command**: `/admin config set-message`
**Steps**:
1. Set custom inactive DM message
2. Set custom archive DM message
3. Set custom training policy message
4. Verify messages are used when performing relevant actions

---

## Phase 9: Error Handling & Edge Cases

### 9.1 Permission Testing
**Steps**:
1. Attempt admin commands without proper role (should error gracefully)
2. Test commands with invalid user inputs
3. Test with non-existent users/IDs

### 9.2 Data Integrity
**Steps**:
1. Test assignment creation with already-assigned student
2. Test waitlist operations with invalid data
3. Verify proper error messages for all failure scenarios

---

## Expected Behaviors & Validation Points

### Success Indicators:
- All commands execute without errors
- Appropriate confirmation messages displayed
- Database updates reflected in embeds
- Notifications sent to relevant users
- Proper error handling for invalid operations

### Key Validations:
- ✅ Students properly move through waitlist → assignment → training cycle
- ✅ Instructor capacity limits respected
- ✅ OTS workflow functions correctly
- ✅ Reports generate accurate data
- ✅ Form system operates end-to-end
- ✅ Notice board updates dynamically
- ✅ Permission checks enforce security

### Critical Issues to Report:
- Commands failing with errors
- Missing confirmations or notifications
- Embeds not updating after operations
- Permission bypasses
- Data inconsistencies between commands and reports

---

## Post-Testing Checklist

After completing all tests:
- [ ] All dynamic embeds display current data
- [ ] Training workflow operates smoothly
- [ ] All reports generate successfully
- [ ] Form submissions can be managed
- [ ] Notice board functions properly
- [ ] OTS system works end-to-end
- [ ] Student progression tracking accurate
- [ ] Instructor capacity management functional

- [ ] Error handling appropriate for all scenarios
