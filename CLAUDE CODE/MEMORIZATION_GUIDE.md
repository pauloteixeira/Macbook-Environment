# MEMORIZATION GUIDE
Abaixo tem uma meneira de adicionar a memoria no mempalace sem precisar consumir tokens.

Via terminar execute um comando como (dentro da past: cd ~/Documents/www/.mempalace/notes/nfse):

```vim
cat <<'EOF' > mem_SUBJECT_NAME.md
# [doctor-nfse] Config Tax Rules API — Architecture and Business Rules

## Summary
We implemented a backend API for managing config_tax_rules scoped under professional and company.

## Key decisions
- All routes are nested under `/professional/:professional_id/company/:company_id/rule`
- Every request must validate that the company belongs to the professional
- rules is stored as JSON string but returned parsed
- Cannot delete or deactivate the last active rule
- PATCH toggles is_active

## Important details
- Controller validates ownership
- Service scoped by company_id
- Active rule guard uses count excluding current
- Responses always return parsed JSON

## Why this matters
Prevents cross-professional access and ensures at least one active rule.

## Tags
doctor-nfse tax-rules, backend, authorization, nfse
EOF
```

Em seguida execute o comando:
```bash
mempalace mine .mempalace
```

E quando fizer seus prompts no modo agente use algo como: `Search mempalace memory for doctor-nfse tax rules implementation`

## RESUMED DESCRIPTION

Save this as a long-term project memory.

Title: [doctor-nfse] Config Tax Rules API — Architecture and Business Rules

Summary:
We implemented a backend API for managing config_tax_rules scoped under professional and company.

Key decisions:

* All routes are nested under `/professional/:professional_id/company/:company_id/rule`
* Every request must validate that the company belongs to the professional before any operation
* `rules` field is stored as JSON string in DB but always parsed in API responses
* Business rule: cannot delete or deactivate a rule if it is the last active rule for the company
* PATCH is used to toggle `is_active`

Important implementation details:

* Controller enforces ownership validation via `assertCompanyBelongsToProfessional`
* Service is always scoped by `company_id`
* Guard for active rules uses count query excluding current rule
* Responses always return parsed JSON for `rules`

Why this matters:
This prevents cross-professional data access and ensures at least one active tax rule always exists per company.

Tags:
doctor-nsfse tax-rules, backend, authorization, business-rules, nfse
