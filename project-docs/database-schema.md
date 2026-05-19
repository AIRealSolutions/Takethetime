# Database Schema Planning — Take the Time

## Purpose

This document defines the first-pass database structure for the MVP.

The schema should support:

- artist-created templates
- customer personalization
- proof approval workflows
- guided sessions
- production and fulfillment
- future scaling

---

# Core Tables

## customers

Purpose:

Store customer contact information.

Suggested fields:

- id
- first_name
- last_name
- email
- phone
- created_at
- notes

---

## templates

Purpose:

Store artist-created card templates.

Suggested fields:

- id
- title
- slug
- collection_id
- description
- orientation
- card_size
- artwork_url
- thumbnail_url
- active
- created_at

---

## template_collections

Purpose:

Organize templates by emotional category.

Suggested fields:

- id
- name
- slug
- description
- featured_image
- active

---

## template_editable_zones

Purpose:

Define approved editable areas.

Suggested fields:

- id
- template_id
- zone_name
- zone_type
- x_position
- y_position
- width
- height
- character_limit
- required

---

## orders

Purpose:

Track customer requests and production workflow.

Suggested fields:

- id
- customer_id
- status
- subtotal
- shipping_total
- total
- delivery_method
- proof_status
- created_at

---

## order_items

Purpose:

Store individual customized cards.

Suggested fields:

- id
- order_id
- template_id
- quantity
- print_option
- review_requested
- fulfillment_type

---

## card_customizations

Purpose:

Store customer-written personalization.

Suggested fields:

- id
- order_item_id
- recipient_name
- sender_name
- message_content
- closing_line
- font_selection
- color_selection
- created_at

---

## uploaded_assets

Purpose:

Store uploaded customer photos.

Suggested fields:

- id
- order_item_id
- asset_url
- asset_type
- approved
- uploaded_at

---

## proofs

Purpose:

Track proof generation and approval.

Suggested fields:

- id
- order_item_id
- proof_url
- proof_version
- approved
- approved_at
- revision_notes

---

## guided_sessions

Purpose:

Store artist-guided appointments.

Suggested fields:

- id
- customer_id
- session_type
- session_date
- session_status
- notes
- created_at

---

# Recommended Status Values

## Order Status

- draft
- submitted
- awaiting_review
- proof_sent
- awaiting_approval
- approved_for_print
- printing
- shipped
- delivered

## Proof Status

- not_started
- generated
- awaiting_customer
- revision_requested
- approved

---

# Important Architecture Notes

- Keep templates separate from customer personalization.
- Never allow customers to overwrite original artwork.
- Preserve proof history.
- Preserve customer-written content securely.
- Support future expansion into workshops, subscriptions, and corporate workflows.
