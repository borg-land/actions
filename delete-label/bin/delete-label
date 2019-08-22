#!/bin/bash
set -eu

label_name="$1"

if [[ -z "$GITHUB_TOKEN" ]]; then
  echo "Set the GITHUB_TOKEN env variable."
  exit 1
fi

if [[ -z "$GITHUB_EVENT_NAME" ]]; then
  echo "Set the GITHUB_REPOSITORY env variable."
  exit 1
fi

if [[ -z "$GITHUB_EVENT_PATH" ]]; then
  echo "Set the GITHUB_EVENT_PATH env variable."
  exit 1
fi

URI="https://api.github.com"
API_HEADER="Accept: application/vnd.github.v3+json"
AUTH_HEADER="Authorization: token ${GITHUB_TOKEN}"

action=$(jq --raw-output .action "$GITHUB_EVENT_PATH")
state=$(jq --raw-output .review.state "$GITHUB_EVENT_PATH")
number=$(jq --raw-output .pull_request.number "$GITHUB_EVENT_PATH")


delete_label() {

   if [[ "$(jq --raw-output .labels.name "$GITHUB_EVENT_PATH")" == "$label_name" ]]; then
      echo "Deleting label from Pull Request"
        curl -sSL \
        -H "${AUTH_HEADER}" \
        -H "${API_HEADER}" \
        -X DELETE \
        "${URI}/repos/${GITHUB_REPOSITORY}/issues/${number}/labels/${label_name}"
      break
    fi
      
}

if [[ "$action" == "dismissed" ]]; then
  delete_label
else
  echo "Ignoring event ${action}/${state}"
  exit 78
fi