This command will dump route53 records "Name","Type","Value","TTL" 

aws route53 list-resource-record-sets --hosted-zone-id "/hostedzone/xxxxxxxxxxx" --profile aws-profile --output json | jq -r '["Name", "Type", "Value" , "TTL"], (.ResourceRecordSets[] | [.Name, .Type, (.ResourceRecords | select(. != null) | map(.Value) | join(" ")), (.AliasTarget.DNSName? | select(. != null)), ."TTL"]) | @csv'
