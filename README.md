Providers Platform

This repository contains the frontend application for the Exoticca Providers Platform. This tool enables local partners and providers to manage their services, view bookings, and create traveler-facing documents.

Key Features

Bookings Management: View and filter all upcoming bookings.

Arrivals Dashboard: Track all incoming traveler arrivals in one place.

Document Builder: A powerful tool for creating, previewing, and submitting custom documents for approval.

Welcome Letter Creator

Daily Schedule Creator

Document Management: Track the status of all submitted documents (In Progress, In Review, Approved, Cancelled).

Document Builder Automation Flows

The Document Builder is designed to automate the creation and delivery of essential traveler documents. Here are the primary automation flows:

1. Document Creation & Preview Flow (Provider-Facing)

This flow allows a provider to easily create a new document from a template.

Select Type: The provider navigates to "Document Builder" and chooses a document type (e.g., "Welcome Letter" or "Schedule").

Configure: The provider fills in the main configuration:

Language

Applicable Itineraries

Auto-upload Schedule (e.g., d-60, d-30)

Add Content: The provider fills in the template.

For Welcome Letters: They fill in the collapsible sections (Arrival, Hotels, Packing, etc.). Standard content (like the intro and app info) is automatically included.

For Schedules: They use the dynamic table to add/remove days and fill in the itinerary for each day.

Live Preview: At any time, the provider can click "Preview". The system instantly generates a live, pixel-perfect preview of the final PDF, including the Exoticca branding and all standard/custom content.

Submit: Once satisfied, the provider clicks "Send for Approval". This action logs the document in the "Documents" section with the status In Review.

2. Document Approval Workflow (Internal-Facing)

This flow manages the document status after submission, ensuring quality control.

Submission: A provider submits a document. The system status changes to In Review.

Notification (Implied): An internal Exoticca team is notified that a new document is ready for review.

Review: The internal team reviews the document for accuracy, tone, and branding.

Status Change: The internal team marks the document as:

Approved: The document is finalized and locked, ready for the final automation step.

Cancelled / Rejected: The document is rejected. The provider sees this status in their "Documents" list and can "Amend" (which creates a new version) or "Cancel" it.

Provider View: The provider sees the new status (Approved, Cancelled) in their "Documents" list.

3. Automated Traveler-Facing Upload (Backend Flow)

This is the primary automation that connects the provider's approved document to the end-traveler.

Configuration: This flow relies on the "Auto-upload Schedule" (d-60, d-30, d-15) set during the document's creation.

Monitoring: A backend scheduler (e.g., a cron job) runs daily.

Action Trigger: The scheduler queries for all Approved documents. It compares the document's "Auto-upload Schedule" against the departure dates of all bookings for the "Itineraries Applicable."

Example:

A "Norway Welcome Letter" is Approved for itinerary N-123 with a schedule of d-30.

Today is October 31st.

The scheduler finds all bookings for N-123 departing on November 30th (30 days from now).

Final Automation: For all matching bookings, the system automatically uploads the finalized PDF, making it visible to the traveler via the Exoticca App and/or sending it via email. This requires zero manual intervention from the provider or the internal team after approval.