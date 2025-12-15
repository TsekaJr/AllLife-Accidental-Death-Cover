# AllLife R25k Accidental Death Cover - Lead Generation Platform

**Version:** 1.0.0  
**Status:** Frontend Complete / Ready for Backend Integration  
**Lead Developer:** Junior Tseka (Lead Generation)

## Project Overview

This is a standalone, responsive landing page designed to capture high-quality leads for the **R25,000 Free 12-Month Accidental Death Cover** campaign. 

The platform features advanced client-side validation to ensure data integrity before submission, a "Funeral Cost Estimator" tool to drive engagement and a 3-stage data capture strategy to minimize lead drop-off.

## Key Features

* **Bank-Grade Validation:** Implements the **Luhn Algorithm** to mathematically verify South African ID numbers, ensuring no fake or typo-ridden IDs are submitted.
* **"Gatekeeper" Eligibility Logic:** A secondary check runs on submission to reject users who do not meet Age (18-75), Salary (R10k+) or Citizenship criteria.
* **3-Stage Data Capture:**
    1.  **Partial Lead:** Captures contact info immediately upon qualification (Stage 2).
    2.  **Full Application:** Captures ID and policy details (Stage 3).
    3.  **Referral:** Captures friend referrals on the success page.
* **Mobile-First UX:** Optimized for South African mobile devices, including a specific "Funeral Calc" mobile view and sticky CTA buttons.
* **Interactive Tools:** Integrated Funeral Cost Estimator with dynamic calculations.

## Technical Stack

* **Frontend:** HTML5, Vanilla JavaScript (ES6+)
* **Styling:** Tailwind CSS (Compiled to `src/output.css`)
* **Assets:** Optimized images in `/images` folder
* **External Dependencies:** None (Zero-dependency architecture for speed and security)

---

## API Integration Guide

The frontend is built with "Mock API Hooks" ready to be replaced with real endpoints. Please see the JavaScript `fetch` placeholders in `index.html`.

### 1. Partial Lead Capture (Drop-Off Protection)
* **Trigger:** User clicks "Activate" after passing the initial status check.
* **Purpose:** Recover abandoned carts if user drops off at the ID stage.
* **Payload:**
    ```json
    {
      "phone": "0821234567",
      "salaryBracket": "10k-19k",
      "age": 35,
      "citizen": "yes",
      "email": "user@example.com",
      "altPhone": "0720000000",
      "stage": "DropOff_After_Qualification"
    }
    ```

### 2. Full Application Submission
* **Trigger:** User clicks "Activate My Cover" on the final form.
* **Validation:** Fires only after ID Luhn check and Gatekeeper logic pass.
* **Payload:**
    ```json
    {
      "firstName": "John",
      "lastName": "Doe",
      "idNumber": "9001015000087",
      "dob": "1990-01-01",
      "phone": "0821234567",
      "altPhone": "0720000000",
      "email": "user@example.com",
      "incomeBracket": "10k-19k",
      "isCitizen": "yes",
      "termsAccepted": true,
      "source": "R25k_Free_Cover_Campaign"
    }
    ```

### 3. Referral Submission
* **Trigger:** User submits the "Refer a Loved One" form on the success page.
* **Payload:**
    ```json
    {
      "referrerId": "9001015000087", 
      "friendName": "Jay Tseka",
      "friendContact": "0829998888",
      "friendEmail": "jay@example.com"
    }
    ```

---

## Security & Validation Details

### ID Number Validation
The system uses a strict implementation of the **Luhn Algorithm (Mod 10)**.
* It does **not** rely on a database lookup (protecting API costs).
* It mathematically verifies the check-digit (13th number).
* It cross-references the birth date (First 6 digits) with the valid calendar.

### Eligibility "Gatekeeper"
The final submit button runs a synchronous check against campaign rules:
* **Age:** Must be 18 - 75.
* **Income:** Must be > R10,000/pm.
* **Citizenship:** Must be South African.
* *Action:* If rules are violated, the form blocks submission and displays a specific error message.

---

## Note to the Development Team

I have built this frontend with a focus on user experience and data validation. However, coming from a Lead Gen background, I have a strong interest in deepening my technical skills.

**I am very open to feedback.** If you spot areas for optimization, better security practices, or cleaner code structure during the integration phase, I would appreciate your suggestions. I am eager to learn from your expertise to align my future builds with your internal standards.

## Contact

**Lead Developer:** Junior Tseka (Lead Gen)


## File Structure

/
├── index.html          # Main application file
├── README.md           # This documentation
├── docs/
│   └── 2024.pdf        # Terms & Conditions (PDF)
├── src/
│   └── output.css      # Tailwind compiled CSS
└── images/
    ├── alllife_logo.png
    ├── casket.jpg
    ├── funeral4.jpg
    └── ... (other assets)
