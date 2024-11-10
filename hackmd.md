# Food2gether
*A collaborative ordering system designed to simplify group orders for large teams.*

---

## Team Members

- **Marvin**: Backend Development, Organization
- **Nikolas**: Backend Development
- **Kaan**: Backend Development
- **Robin**: Frontend Development
- **Jo**: Wildcard (Flexible Role)

---

## Libraries and Tools

- **OpenStreetMap / Leaflet**: For map integration
    - [Leaflet Tutorials](https://leafletjs.com/examples.html)
- **PayPal**: For payment processing
    - [PayPal Developer](https://developer.paypal.com/home/)
    - [PayPal REST API](https://developer.paypal.com/api/rest/)
- **Quarkus & Quarkus Web/REST**: For backend framework
    - [Quarkus OpenConnect Documentation](https://quarkus.io/guides/security-openid-connect-providers#google)
- **Keycloak**: For authentication and authorization

---

## Roles

- **Participants** – Users who join sessions and place orders
- **Interested** - Users who join sessions without placing an order
- **Organizers** – Users who manage sessions and orders
- **Admin** – (Optional) Advanced management capabilities

---

## Feature Requirements

### Authentication

- **Login Screen**
  - Login options: Google, GitHub, Facebook, Apple, classic email/password
  - Keycloak integration for identity management

### Ordering Sessions

- **Session Management**
  - Create, edit, close, and join sessions
  - View all orders in a session
  - View individual orders
  - Assign payment responsibilities
  - Set a deadline for orders
  - Optional: Tips feature
  - Optional: Private sessions (invite-only)

### Restaurants

- **Restaurant Listings and Menus**
  - Add, edit, and display restaurant menus
  - Optional: Use computer vision for menu recognition
- **Location and Map Integration**
  - Embed maps with restaurant locations
- **Notifications** (Optional)
  - Order arrival notification
  - Unpaid order reminder
  - Deadline reminder

### Ordering

- **Order Management**
  - Place orders within a session
  - Edit and remove orders
  - Overview of current orders

### Payment

- **Payment Options**
  - PayPal integration, QR code for easy access
  - Optional: Direct link to PayPal.me
- **Payment Confirmation**
  - Track and confirm payment status

### Democratic Sessions (Optional)

- **Voting and Suggestions**
  - Vote on session-specific decisions
  - Propose suggestions within sessions

### Platform

- **Web Application**
  - (Potentially consider a mobile app in the future)

---

### Usefull Links

- https://www.youtube.com/watch?v=lsMQRaeKNDk
- https://www.youtube.com/watch?v=CdBtNQZH8a4

