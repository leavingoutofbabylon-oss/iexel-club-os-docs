# IEXEL Club OS Discovery Report

## 1. Repository Structure & Modules

The application is structured around a core and domain modules.

**Modules found (36):**
- Activity
- Attendance
- Authentication
- Branding
- Communications
- Container
- Dashboard
- Database
- EntityLifecycle
- EventAudience
- EventProgress
- Events
- Experience
- Finance
- FootballStatistics
- Logging
- MatchMode
- Modules
- People
- Permissions
- Portal
- Projects
- Registrations
- Relationships
- Release
- SeasonPlanning
- Seasons
- Settings
- Statistics
- TeamAssignments
- Teams
- UI
- Upgrade
- Users
- Venues
- Weather

## 2. Database Table Inventory

**Tables identified (42):**
- `iexel_club_activity_log` (from app/core/Database/DatabaseManager.php)
- `iexel_club_attendance` (from app/core/Database/DatabaseManager.php)
- `iexel_club_club_projects` (from app/core/Database/DatabaseManager.php)
- `iexel_club_communication_attachments` (from app/core/Database/DatabaseManager.php)
- `iexel_club_communication_deliveries` (from app/core/Database/DatabaseManager.php)
- `iexel_club_communication_events` (from app/core/Database/DatabaseManager.php)
- `iexel_club_communication_recipients` (from app/core/Database/DatabaseManager.php)
- `iexel_club_communication_templates` (from app/core/Database/DatabaseManager.php)
- `iexel_club_communications` (from app/core/Database/DatabaseManager.php)
- `iexel_club_event_audience` (from app/core/Database/DatabaseManager.php)
- `iexel_club_event_availability` (from app/core/Database/DatabaseManager.php)
- `iexel_club_event_match_action_requests` (from app/core/Database/DatabaseManager.php)
- `iexel_club_event_match_details` (from app/core/Database/DatabaseManager.php)
- `iexel_club_event_match_incidents` (from app/core/Database/DatabaseManager.php)
- `iexel_club_event_match_lineups` (from app/core/Database/DatabaseManager.php)
- `iexel_club_event_match_player_ratings` (from app/core/Database/DatabaseManager.php)
- `iexel_club_event_match_reports` (from app/core/Database/DatabaseManager.php)
- `iexel_club_event_match_selections` (from app/core/Database/DatabaseManager.php)
- `iexel_club_events` (from app/core/Database/DatabaseManager.php)
- `iexel_club_finance_accounts` (from app/core/Database/DatabaseManager.php)
- `iexel_club_finance_billing_run_items` (from app/core/Database/DatabaseManager.php)
- `iexel_club_finance_billing_runs` (from app/core/Database/DatabaseManager.php)
- `iexel_club_finance_billing_schedules` (from app/core/Database/DatabaseManager.php)
- `iexel_club_finance_discount_policies` (from app/core/Database/DatabaseManager.php)
- `iexel_club_finance_fee_rules` (from app/core/Database/DatabaseManager.php)
- `iexel_club_finance_invoice_events` (from app/core/Database/DatabaseManager.php)
- `iexel_club_finance_invoice_lines` (from app/core/Database/DatabaseManager.php)
- `iexel_club_finance_invoices` (from app/core/Database/DatabaseManager.php)
- `iexel_club_finance_payment_allocations` (from app/core/Database/DatabaseManager.php)
- `iexel_club_finance_payments` (from app/core/Database/DatabaseManager.php)
- `iexel_club_formation_template_slots` (from app/core/Database/DatabaseManager.php)
- `iexel_club_formation_templates` (from app/core/Database/DatabaseManager.php)
- `iexel_club_people` (from app/core/Database/DatabaseManager.php)
- `iexel_club_person_relationships` (from app/core/Database/DatabaseManager.php)
- `iexel_club_person_roles` (from app/core/Database/DatabaseManager.php)
- `iexel_club_player_registrations` (from app/core/Database/DatabaseManager.php)
- `iexel_club_seasons` (from app/core/Database/DatabaseManager.php)
- `iexel_club_system_flags` (from app/core/Database/DatabaseManager.php)
- `iexel_club_team_assignments` (from app/core/Database/DatabaseManager.php)
- `iexel_club_team_seasons` (from app/core/Database/DatabaseManager.php)
- `iexel_club_teams` (from app/core/Database/DatabaseManager.php)
- `iexel_club_venues` (from app/core/Database/DatabaseManager.php)

## 3. Capability Inventory

**Custom Capabilities (18):**
- `iexel_archive_club_projects`
- `iexel_coach_portal`
- `iexel_create_club_projects`
- `iexel_edit_club_projects`
- `iexel_manage_assigned_team`
- `iexel_manage_billing`
- `iexel_manage_club_os`
- `iexel_manage_club_project_visibility`
- `iexel_manage_finance`
- `iexel_manage_match_reports`
- `iexel_manage_people`
- `iexel_manage_welfare`
- `iexel_record_payments`
- `iexel_view_club_projects`
- `iexel_view_finance`
- `iexel_view_player_statistics`
- `iexel_view_welfare`
- `upload_files`

## 4. Route & Request Action Inventory

**Admin Post / AJAX Handlers (19):**
- `iexel_add_person_relationship` (admin_post)
- `iexel_branding_save` (admin_post)
- `iexel_club_os_login` (admin_post_nopriv)
- `iexel_club_os_logout` (admin_post)
- `iexel_club_os_lost_password` (admin_post_nopriv)
- `iexel_club_project_` (admin_post)
- `iexel_communication_action` (admin_post)
- `iexel_communication_template` (admin_post)
- `iexel_entity_lifecycle` (admin_post)
- `iexel_entity_media_save` (admin_post)
- `iexel_finance_` (admin_post)
- `iexel_member_experience_switch` (admin_post)
- `iexel_registration_autosave` (wp_ajax)
- `iexel_remove_person_relationship` (admin_post)
- `iexel_save_communication` (admin_post)
- `iexel_set_billing_contact` (admin_post)
- `iexel_team_assignment_create` (admin_post)
- `iexel_team_assignment_delete` (admin_post)
- `iexel_team_assignment_update` (admin_post)

## 5. Known Placeholders & Technical Debt

**Technical Debt Candidates (79):**
- `app/People/PeopleRepository.php:95` - $placeholders = implode( ', ', array_fill( 0, count( $ids ), '%d' ) );
- `app/People/PeopleRepository.php:96` - return $wpdb->get_results( $wpdb->prepare( "SELECT * FROM {$db->table( 'people' )} WHERE id IN ({$placeholders}) ORDER BY id", ...$ids ), ARRAY_A ) ?: array(); // phpcs:ignore WordPress.DB.PreparedSQL.InterpolatedNotPrepared
- `app/TeamAssignments/TeamAssignmentRepository.php:243` - $placeholders = implode( ', ', array_fill( 0, count( $roles ), '%s' ) );
- `app/TeamAssignments/TeamAssignmentRepository.php:250` - AND ta.assignment_role IN ({$placeholders}){$status_sql}
- `app/TeamAssignments/TeamAssignmentRepository.php:265` - $placeholders = implode( ', ', array_fill( 0, count( $roles ), '%s' ) );
- `app/TeamAssignments/TeamAssignmentRepository.php:272` - AND assignment.assignment_role IN ({$placeholders}){$status_sql}";
- `app/core/Attendance/AttendanceRepository.php:147` - $placeholders = implode( ', ', array_fill( 0, count( $event_ids ), '%d' ) );
- `app/core/Attendance/AttendanceRepository.php:161` - WHERE audience.event_id IN ({$placeholders})
- `app/core/Attendance/AvailabilityRepository.php:103` - $placeholders = implode( ', ', array_fill( 0, count( $event_ids ), '%d' ) );
- `app/core/Attendance/AvailabilityRepository.php:118` - WHERE ea.event_id IN ({$placeholders})
- `app/core/Attendance/AvailabilityRepository.php:149` - AND event_id IN ({$placeholders})",
- `app/core/Branding/BrandingService.php:14` - 'default_member_image_id' => array( 'label' => 'Default member placeholder', 'min_width' => 300, 'min_height' => 300 ),
- `app/core/Branding/BrandingService.php:15` - 'default_team_image_id' => array( 'label' => 'Default Team placeholder', 'min_width' => 600, 'min_height' => 400 ),
- `app/core/Communications/CommunicationAudienceResolver.php:39` - $placeholders = implode( ',', array_fill( 0, count( $roles ), '%s' ) );
- `app/core/Communications/CommunicationAudienceResolver.php:40` - return $wpdb->get_results( $wpdb->prepare( "SELECT DISTINCT p.id AS person_id,p.display_name AS name,p.email,r.role_key AS recipient_role,NULL AS team_id,NULL AS season_id,NULL AS relationship_context FROM {$this->db->table( 'people' )} p INNER JOIN {$this->db->table( 'person_roles' )} r ON r.person_id=p.id AND r.status='active' WHERE p.status='active' AND r.role_key IN ({$placeholders}) ORDER BY p.display_name", ...$roles ), ARRAY_A ) ?: array();
- `app/core/Events/EventRepository.php:150` - $team_placeholders = implode( ', ', array_fill( 0, count( $team_ids ), '%d' ) );
- `app/core/Events/EventRepository.php:166` - WHERE event.team_id IN ({$team_placeholders})
- `app/core/Finance/BillingAudienceResolver.php:59` - $placeholders = implode( ',', array_fill( 0, count( $person_ids ), '%d' ) );
- `app/core/Finance/BillingAudienceResolver.php:60` - $people = $wpdb->get_results( $wpdb->prepare( "SELECT id,display_name,date_of_birth,status FROM {$this->db->table( 'people' )} WHERE id IN ($placeholders)", ...$person_ids ), ARRAY_A ) ?: array(); // phpcs:ignore WordPress.DB.PreparedSQL.InterpolatedNotPrepared
- `app/core/Finance/BillingAudienceResolver.php:63` - $roles = $wpdb->get_results( $wpdb->prepare( "SELECT person_id,role_key,status FROM {$this->db->table( 'person_roles' )} WHERE person_id IN ($placeholders)", ...$person_ids ), ARRAY_A ) ?: array(); // phpcs:ignore WordPress.DB.PreparedSQL.InterpolatedNotPrepared
- ... and 59 more items.
