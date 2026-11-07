# 🤖 Aradhya ERP — Interactive WhatsApp Action Bot & WhatsMsg Gateway

<div align="center">

[![WhatsApp](https://img.shields.io/badge/WhatsApp-Interactive_Bot-25D366?style=for-the-badge&logo=whatsapp&logoColor=white)](https://wa.me/919955882299?text=Hi!+I%27m+interested+in+Aradhya+ERP)
[![Powered by WhatsMsg](https://img.shields.io/badge/Powered_by-WhatsMsg.in-25D366?style=for-the-badge&logo=whatsapp&logoColor=white)](https://whatsmsg.in/)
[![ERP Integration](https://img.shields.io/badge/Aradhya_ERP-Live_Sync-1e315a?style=for-the-badge)](https://aradhyaerp.in)
[![License](https://img.shields.io/badge/License-Proprietary_SaaS-orange?style=for-the-badge)](https://aradhyaerp.in)

**Instant WhatsApp-Based Student Self-Service for Parents & Schools**  
*Check Fees, Pay Online via UPI, Check Daily Attendance, View Homework & Read Notices Directly in WhatsApp powered by [WhatsMsg](https://whatsmsg.in/).*

[🚀 Official Website](https://aradhyaerp.in) • [💬 WhatsMsg Gateway](https://whatsmsg.in/) • [💳 Pricing Plans](https://aradhyaerp.in/#pricing) • [📖 Documentation](https://github.com/aradhyaerp/school-management-system-docs) • [📞 Contact](https://aradhyaerp.in/contact-us)

</div>

---

## 🌟 Overview

The **Aradhya ERP WhatsApp Action Bot** connects parents directly to their school's live ERP database through conversational WhatsApp commands powered by [WhatsMsg](https://whatsmsg.in/). Parents don't need to remember usernames, passwords, or open a browser—they simply send natural commands like `/fees` or `/attendance` from their registered mobile number!

### 🔄 Architecture Flow

```
┌─────────────────┐       /fees        ┌───────────────────────┐
│ Parent WhatsApp │ ─────────────────> │ WhatsMsg Action Bot   │
│  (Mobile Phone) │                    │ (https://whatsmsg.in) │
└─────────────────┘                    └───────────┬───────────┘
         ▲                                         │
         │                              HTTP GET /fees?phone=...
         │                                         ▼
         │                             ┌───────────────────────┐
         │     Formatted Reply         │ Aradhya ERP API       │
         └──────────────────────────── │ (Multi-Tenant Engine) │
               (Fee Dues + UPI Link)   └───────────────────────┘
```

---

## 💬 Supported Bot Commands

| Command | Action ID | Description | Sample Parent Experience |
|:---|:---|:---|:---|
| `/fees` <br>`/fees [adm_no]` | `fees-query` | Returns real-time fee dues, due date, status, and direct UPI payment link. | `*DPS Academy - Fee Status*`<br>`*Student:* Parth Babu`<br>`*Adm No:* AC0001`<br>`*Due Amount:* ₹11,400.00`<br>`*Pay Online:* https://aradhyaerp.in/pay/dps/fees` |
| `/attendance` <br>`/attendance [adm_no]` | `attendance-query` | Returns today's in-time, punch status, and month-to-date attendance percentage. | `*DPS Academy - Attendance*`<br>`*Today's Status:* Present`<br>`*In-Time:* 08:15 AM`<br>`*Month Attendance:* 94% (21 Days)` |
| `/homework` | `homework-query` | Returns today's active homework and class assignments. | `*DPS Academy - Homework (07-Nov-2026)*`<br>`Math: Ch 5 Ex 5.2 (Q1-Q10)`<br>`Science: Revise Plants Diagram` |
| `/notice` | `notice-query` | Fetches the latest circular, holiday notice, or examination announcement with attachment link. | `*DPS Academy - Circular*`<br>`*Parent Teacher Meeting (PTM)*`<br>`Date: 12-Nov-2026`<br>`Attachment: https://aradhyaerp.in/notices/ptm.pdf` |
| `/help` | `help-query` | Displays the interactive menu of all available bot commands. | Interactive guidance menu in Hindi/Hinglish. |

---

## 📂 Repository Contents

```
├── actions.json               # Complete Actions JSON schema for WhatsMsg (https://whatsmsg.in/) Action Bot
├── README.md                  # Integration & configuration guide
├── controllers/               # Sample Laravel controller & middleware reference
└── schemas/                   # JSON schema definitions
```

---

## ⚙️ How It Works: Actions JSON Breakdown

The [`actions.json`](./actions.json) file defines the mapping between incoming WhatsApp message triggers and backend ERP endpoints via [WhatsMsg](https://whatsmsg.in/):

### 1. Dynamic Parameter Interpolation
- `{{session.id}}` — [WhatsMsg](https://whatsmsg.in/) WhatsApp instance session identifier.
- `{{sender.id}}` — WhatsApp JID of the parent (e.g. `919955882299@s.whatsapp.net`).
- `{{sender.phone}}` — Normalized mobile number of the sender.
- `{{args.0}}` — First argument passed after the command (e.g., in `/fees 1024`, `args.0` is `1024`).

### 2. Smart Phone Matching
If a parent messages from their registered WhatsApp number, they **do not need to enter an admission number**—the ERP automatically identifies all linked wards (students) associated with `father_phone`, `mother_phone`, or `guardian_phone`!

### 3. Online Fee Payment Pipeline
When parents receive the fee message, it includes a secure one-tap payment URL:
```
https://aradhyaerp.in/pay/{school-slug}/fees?adm={admission_no}
```
- Opens mobile-optimized checkout.
- Renders dynamic UPI QR code with school merchant VPA (e.g., `school@upi`).
- Provides 1-tap intent to open **GPay, PhonePe, or Paytm**.
- Submits UTR number with instant receipt confirmation.

---

## 🛡️ Security & Multi-School Isolation

- **Tenant Isolation:** Every incoming webhook is validated by `VerifyWhatsMsgMultiSchoolBot` middleware.
- **Session Verification:** Only authorized [WhatsMsg](https://whatsmsg.in/) sessions mapped to the specific school can fetch data.
- **Rate Limiting:** Ingress throttling protects the ERP from message flooding or spam.

---

## 💎 Pricing & Availability

The Interactive WhatsApp Bot powered by [WhatsMsg](https://whatsmsg.in/) is included in Aradhya ERP plans:
- **Starter Plan (₹5/student):** Available as an add-on (@ ₹2,000/month).
- **Standard Plan (₹10/student):** ✅ **Fully Included** (WhatsMsg alerts + Interactive Bot).
- **Premium Plan (₹15/student):** ✅ **Fully Included** + Free Custom Designed & Printed ID Cards.

---

## 👨‍💻 Developed & Maintained By

<div align="center">

### 🏢 **[Aradhya Creation](https://aaradhyacreation.in/)**
*Empowering Businesses & Educational Institutions with Cutting-Edge Software Solutions & Creative Technology.*

[![Aradhya Creation Website](https://img.shields.io/badge/Official_Website-aaradhyacreation.in-1e315a?style=for-the-badge&logo=google-chrome&logoColor=white)](https://aaradhyacreation.in/)
[![Aradhya Creation Instagram](https://img.shields.io/badge/Instagram-@aradhya__creation-E4405F?style=for-the-badge&logo=instagram&logoColor=white)](https://www.instagram.com/aradhya_creation)

<br>

### 👤 **Rohan Kumar** *(Lead Developer & Founder)*

[![LinkedIn](https://img.shields.io/badge/LinkedIn-rohansingh62-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/rohansingh62)
[![Instagram](https://img.shields.io/badge/Instagram-@rohansingh__62-E4405F?style=for-the-badge&logo=instagram&logoColor=white)](https://www.instagram.com/rohansingh_62)

</div>

---

## 📞 Support & Setup Assistance

For assistance connecting your school's WhatsApp number to Aradhya ERP via [WhatsMsg](https://whatsmsg.in/):
- 🌐 **Aradhya ERP:** [https://aradhyaerp.in](https://aradhyaerp.in)
- 🏢 **Company Portal:** [https://aaradhyacreation.in/](https://aaradhyacreation.in/)
- 💬 **WhatsMsg Gateway:** [https://whatsmsg.in/](https://whatsmsg.in/)
- 📱 **WhatsApp Support:** [+91 9955882299](https://wa.me/919955882299?text=Hi!+I%27m+interested+in+Aradhya+ERP+WhatsMsg+Bot)
- 📞 **Phone:** [+91 9955882299](tel:+919955882299)
- 📍 **Headquarters:** Motihari, Bihar, India
- ✉️ **Email:** [support@aradhyaerp.in](mailto:support@aradhyaerp.in)

<div align="center">

---

**© 2026 [Aradhya ERP Technologies](https://aradhyaerp.in) & [WhatsMsg](https://whatsmsg.in/). Developed with ❤️ by [Aradhya Creation](https://aaradhyacreation.in/) & [Rohan Kumar](https://www.linkedin.com/in/rohansingh62). All rights reserved.**  
*Empowering Education with Intelligent Automation.*

</div>
