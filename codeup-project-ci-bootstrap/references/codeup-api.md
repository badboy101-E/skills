# Codeup API

## Platform assumptions

This skill targets central-edition Codeup.

- OpenAPI domain default: `openapi-rdc.aliyuncs.com`
- Git host default: `codeup.aliyun.com`
- organization id: supply per user, per org, or per environment

## Authentication

Read the token from the local `.env` file:

```env
YUNXIAO_TOKEN=...
```

Send it in the request header:

```text
x-yunxiao-token: <YUNXIAO_TOKEN>
```

## Create repository endpoint

Use the central-edition create repository endpoint:

```text
POST https://<openapi_domain>/oapi/v1/codeup/organizations/<organization_id>/repositories
```

## Default repository settings

- visibility: `private`
- default branch: `main`
- no namespace unless the user later introduces one
- no remote README initialization unless explicitly requested

## Public skill guidance

If this skill is shared publicly:

- do not ship a real personal `organization_id`
- treat `organization_id` as a required runtime parameter
- present `openapi-rdc.aliyuncs.com` and `codeup.aliyun.com` as central-edition defaults, not universal constants

## Repository name source

Use the local folder name as the default repository name, then normalize it as needed for remote creation.
