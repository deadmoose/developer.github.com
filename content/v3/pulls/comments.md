---
title: Pull Request Comments API v3 | developer.github.com
---

# Pull Request Comments API

## List comments on a pull request

    GET /repos/:user/:repo/pulls/:id/comments

### Response

<%= headers 200 %>
<%= json(:pull_comment) { |h| [h] } %>

## Get a single comment

    GET /repos/:user/:repo/pulls/comments/:id

### Response

<%= headers 200 %>
<%= json :pull_comment %>

## Create a comment

    POST /repos/:user/:repo/pulls/:id/comments

### Input

body
: _Required_ **string**

commit_id
: _Required_ **string** - Sha of the commit to comment on.

path
: _Required_ **string** - Relative path of the file to comment on.

position
: _Required_ **number** - Line index in the diff to comment on.

#### Example

<%= json \
  :body      => 'Nice change',
  :commit_id => '6dcb09b5b57875f334f61aebed695e2e4193db5e',
  :path      => 'file1.txt',
  :position  => 4,
%>

### Alternative Input

Instead of passing `commit_id`, `path`, and `position` you can reply to
an existing Pull Request Comment like this:

body
: _Required_ **string**

in_reply_to
: _Required_ **number** - Comment id to reply to.

#### Example

<%= json \
  :body        => 'Nice change',
  :in_reply_to => 4,
%>

### Response

<%= headers 201,
      :Location =>
"https://api.github.com/repos/:user/:repo/pulls/comments/1" %>
<%= json :pull_comment %>

## Edit a comment

    PATCH /repos/:user/:repo/pulls/comments/:id

### Input

body
: _Required_ **string**

#### Example

<%= json \
  :body => 'Nice change'
%>

### Response

<%= headers 200 %>
<%= json :pull_comment %>

## Delete a comment

    DELETE /repos/:user/:repo/pulls/comments/:id

### Response

<%= headers 204 %>
