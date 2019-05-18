# mc-aws

Consists of mc server components, a cli tool `mc-server.sh` a user-data for the spot instance and some launch configs.

### How it works:
Request a spot instance based off the provided launch configuration and the arbitrary instance type.

What to look for in terms of server suitable for mc:
0. Computing power
0. Network performance
0. At least 2 gigs of RAM

Satisfiable by a c5/c5d type ec2 instance.
We use spot instance, therefore have to take care of saving and loading the game.
Kinda best choice for this: c5d.large. Relatively cheap, by ca. 70% than usual price, $0.033 + TAX of course.

### Launch config example
```
{
    "SecurityGroupIds": [
        "SC_GROUP_FOR_SSH_AND_PORT_25565"
    ],
    "EbsOptimized": true,
    "IamInstanceProfile": {
        "YOUR_INSTANCE_PROFILE_PREFFEREBLY_TO_FULL_S3_ACCESS"
    },
    "ImageId": "AMI_DEPENDS_ON_THE_REGION",
    "InstanceType": "{instance_type}", // This comes from the cli
    "KeyName": "YOUR_REGISTERED_SSH_KEY",
    "Monitoring": {
        "Enabled": false
    },
    "UserData": "{user_data}" // This also comes from the cli
}
```

Use the cli tool, run `./mc-server.sh` for help, or with help, or --help doesn't really matter. 
