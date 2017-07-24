# Conceptual content prompt

## Add team member

To add a member to a team, the authenticated user must the owner of an organization or have *'admin'* permissions for the team.

If the team member being added is not currently a part of the team's organization, this endpoint will send an invitation by email. This new membership will be in the "pending" state until the invitation is accepted.

If the user is already a member of the team, this endpoint will only update the team member's role. 

### Parameters

| Name | Type | Description |
| ------ | ------ | ------ |
| `role` | `string` | The possible roles of a team member can be one of the following: <br> * `member` - a normal team member. <br>* `maintainer` - a team maintainer. This member is able to add, remove or promote other members to the role of `maintainer`.  This member may also edit the team's name and description. <br> Default: `member` |

### Example

```sh
$ curl https://api.github.com/teams/1/memberships/octocat \
    -X PUT \
    -d '{
            "role": "maintainer"
        }'
```

### Response

```json
{
  "state": "pending",
  "role": "maintainer",
  "url": "https://api.github.com/teams/1/memberships/octocat"
}
```

## Remove team membership
To remove a user from a team, the authenticated user must have *'admin'* permissions for the team or be an owner of the organization.

**NOTE:** This only removes their membership from the team.

### Example

```sh
$ curl https://api.github.com/teams/1/memberships/octocat \
    -X DELETE
```

### Response

```
Status: 204 No Content
```



# Referential content prompt

A user's contribution graph allows you to visualize the density of commits for repositories the user contributed.

## Contributions graph color modification

```
POST /user/:username/contributions/edit
```

### Parameters
| Name | Type | Description |
| ------ | ------ | ------ |
| `date` | `string` | **Required**. Only for this date the color changes for square dot will be changed. This is a timestamp in ISO 8601 format: `YYYY-MM-DDTHH:MM:SSZ` |
| `color` | `string` | A 6 character hex code, without the leading #, identifying the color for the square. The colors can only be <br> * `DarkGreen (006400)` <br> * `ForestGreen (228b22)` <br> * `Green (008000)` <br> * `GreenYellow (adff2f)`. <br> Default: `Green` |

### Example
```json
{
  "date": "2017-07-19T00:00:00Z",
  "color": "006400"
}
```

### Response

```json
Status: 200 OK

{
  "id": 1,
  "url": "https://api.github.com/user/octocat/contributions",
  "date": "2017-07-19T00:00:00Z",
  "color": "006400",
  "default": false
}
```
