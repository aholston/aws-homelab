# AWS Homelab

Welcome to your personal AWS Homelab — a secure, hands-on environment designed to simulate real-world AWS architecture and cloud security practices. This project is built from the ground up to deepen your knowledge, prepare for certifications, and showcase your skills in a clean, well-documented portfolio.

---

## 📌 Purpose

* Learn AWS infrastructure and security fundamentals by doing
* Simulate real-world environments with a focus on secure design
* Document everything for easy recall and future job interviews
* Build a public-facing portfolio of cloud and security skills

---

## 📁 Folder Structure

```
aws-homelab/
├── README.md                      ← Overview of your lab + goals
├── diagrams/                     ← Visuals of architecture and flows
│   └── vpc-architecture.png
├── networking/                   ← Subnet, VPC, and routing design
│   └── vpc-design.md
├── compute/                      ← EC2 setup and server documentation
│   └── ec2-jumpbox.md
├── identity/                     ← IAM structure, users, and policies
│   └── iam-roles.md
├── security/                     ← Logging, monitoring, and detection
│   └── cloudtrail-setup.md
├── simulations/                  ← Attack/incident scenarios + notes
│   └── compromised-user-case.md
└── terraform/ (optional)         ← Infrastructure-as-code configuration
    └── vpc.tf
```

---

## ✅ Current Phase: Network Design

Start by defining the VPC, subnets, route tables, and access boundaries.

* See: `networking/vpc-design.md`

---

## 🚧 Roadmap

* [x] Define VPC + Subnet structure
* [x] Provision VPC and subnets
* [x] Create and associate public route table
* [x] Create and associate private route table
* [ ] Set up IAM users and roles
* [ ] Deploy EC2 jumpbox in public subnet
* [ ] Enable CloudTrail and CloudWatch
* [ ] Create and test access policies
* [ ] Simulate first security event

---

## 🧠 Tips

* Keep each phase modular — clean files, clear boundaries
* Comment your decisions — this is a portfolio, not just a project
* Prioritize realism: security-first, no shortcuts unless noted

---

## 📎 Notes

This homelab is a living project. As you add services (S3, Lambda, WAF, etc.), expand the folder structure and docs to match.

When you’re ready to make it public-facing, you can drop this into GitHub with a polished README and architecture diagram.
