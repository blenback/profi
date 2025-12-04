# CV YAML Data Structure Documentation

This README documents the expected field structure for each YAML file used in the remote CV generation system.

## Overview

The CV system pulls data from individual YAML files hosted on GitHub. Each section of the CV corresponds to a specific YAML file with its own expected structure. All fields should be strings unless otherwise specified.

## File Structure Summary

| YAML File | Purpose | Type | Required Fields |
|-----------|---------|------|-----------------|
| `contact.yaml` | Contact information | Single object | position, institute, city, email, website, orcid, linkedin, github, twitter, researchgate |
| `profile.yaml` | Professional profile/summary | List of objects | text |
| `skills.yaml` | Technical skills | List of objects | subject, level |
| `languages.yaml` | Language skills | List of objects | subject, level |
| `education.yaml` | Educational background | List of objects | degree, university, city, start, end, thesis, awards |
| `experience.yaml` | Work experience | List of objects | position, institute, city, start, end, activities |
| `workshops.yaml` | Teaching & training | List of objects | title, location, start, description, url |
| `awards.yaml` | Grants & funding | List of objects | name, institute, city, date, description, url, link_type |
| `publications.yaml` | Academic publications | List of objects | title, authors, year, journal, volume, pages, doi |
| `oral_presentations.yaml` | Conference presentations | List of objects | title, event, location, date, url |
| `posters.yaml` | Poster presentations | List of objects | title, event, location, date, url |
| `packages.yaml` | R packages | List of objects | package, description, url, cran, version |

---

## Detailed Field Specifications

### 📧 contact.yaml
**Structure:** Single object (not a list)
```yaml
position: "Your job title"
institute: "Your institution (can include markdown links)"
city: "City, Country"
email: "your.email@domain.com"
phone: "Optional phone number (can be empty)"
website: "https://your-website.com"
orcid: "0000-0000-0000-0000"
linkedin: "your-linkedin-username"
github: "your-github-username"
twitter: "your-twitter-handle"
researchgate: "https://www.researchgate.net/profile/Your-Profile"
```

### 👤 profile.yaml
**Structure:** List of objects
```yaml
- text: "Your professional summary/bio text. Can be a long paragraph describing your background, expertise, and interests."
```

### 🛠️ skills.yaml
**Structure:** List of objects
```yaml
- subject: "R (Shiny, Quarto)"
  level: "advanced"
- subject: "Python"
  level: "intermediate"
- subject: "JavaScript"
  level: "basic"
```
**Valid levels:** `advanced`, `intermediate`, `basic`

### 🌐 languages.yaml
**Structure:** List of objects
```yaml
- subject: "English"
  level: "Native"
- subject: "German"
  level: "B2"
```

### 🎓 education.yaml
**Structure:** List of objects
```yaml
- degree: "Doctor of Philosophy (PhD) in Environmental Science"
  university: "University Name"
  city: "City, Country"
  start: "Sep. 2020"
  end: "Jun. 2025"
  description: "Optional description of the program (can be empty)"
  thesis: "[Thesis title with optional link](https://link-to-thesis.com)"
  awards: "Any awards or honors received (can be empty)"
```

### 💼 experience.yaml
**Structure:** List of objects
```yaml
- position: "Job Title"
  institute: "Company/Institution Name"
  city: "City, Country"
  start: "Jan. 2020"
  end: "Dec. 2022"
  activities: "Description of responsibilities and achievements. Can include multiple sentences separated by periods."
```

### 🏫 workshops.yaml
**Structure:** List of objects
```yaml
- title: "Workshop Title"
  location: "City, Country"
  start: "Sep. 2024"
  end: "Optional end date (can be empty)"
  description: "Workshop description"
  url: "https://link-to-workshop-materials.com"
```

### 🏆 awards.yaml
**Structure:** List of objects
```yaml
- name: "Award/Grant Name"
  institute: "Funding Organization"
  city: "City, Country"
  date: "Jun. 2023"
  description: "Description of the award or project funded"
  url: "https://link-to-more-info.com"
  link_type: "website"
```
**Valid link_types:** `website`, `pdf`, `github`, etc.

### 📚 publications.yaml
**Structure:** List of objects
```yaml
- title: "Article Title"
  authors: "Author, A. and Author, B."
  year: "2022"
  journal: "Journal Name"
  volume: "38"
  pages: "e02228"
  doi: "https://10.1016/j.journal.2022.e02228"
  data_url: "https://zenodo.org/record/123456"
  code_url: "Optional GitHub repository (can be empty)"
  preprint_url: "Optional preprint link (can be empty)"
  results_url: "Optional results/supplementary link (can be empty)"
```

### 🎤 oral_presentations.yaml
**Structure:** List of objects
```yaml
- title: "Presentation Title"
  event: "Conference Name"
  location: "City, Country"
  date: "Jun. 2019"
  type: "Optional type field (can be empty)"
  url: "https://link-to-slides.com"
```

### 📋 posters.yaml
**Structure:** List of objects
```yaml
- title: "Poster Title"
  event: "Conference Name (can be empty)"
  location: "City, Country"
  date: "Oct. 2015"
  authors: "Optional author list (can be empty)"
  url: "Optional link to poster (can be empty)"
```

### 📦 packages.yaml
**Structure:** List of objects
```yaml
- package: "Package Name"
  description: "Brief description of what the package does"
  url: "https://github.com/username/packagename"
  cran: false
  version: "1.0.0"
```
**Note:** `cran` field is boolean (true/false)

---

## 📝 General Guidelines

### Date Formatting
Use consistent date formats throughout:
- **Month abbreviations:** `Jan.`, `Feb.`, `Mar.`, `Apr.`, `May`, `Jun.`, `Jul.`, `Aug.`, `Sep.`, `Oct.`, `Nov.`, `Dec.`
- **Format:** `Mon. YYYY` (e.g., `"Sep. 2024"`)

### Markdown Support
The following fields support markdown formatting:
- `institute` in contact.yaml (for links)
- `thesis` in education.yaml (for links)
- All `description` fields
- `title` fields in publications.yaml

### Optional Fields
Fields marked as "can be empty" should still be included in the YAML structure but can have empty string values (`""`).

### Ordering
Entries within each YAML file should be ordered chronologically, with the **most recent items first**. The CV generation system will reverse the order as needed for proper display.

### File Encoding
All YAML files should be saved with UTF-8 encoding to properly handle special characters and international text.

---

## 🔗 Integration

These YAML files are designed to be hosted on GitHub and accessed remotely by the CV generation system. The system expects:

1. **Repository structure:** Each YAML file should be in the root of the repository
2. **File naming:** Exact file names as specified above (e.g., `contact.yaml`, not `contacts.yaml`)
3. **Public access:** Repository should be public or accessible via the GitHub API
4. **Branch:** Files should be on the specified branch (typically `main`)

The CV generation system uses the `read_cv_data_remote()` function to fetch and parse these files automatically.