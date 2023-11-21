aws ec2 create-vpc --cidr-block 10.0.0.0/16 :

{
    "Vpc": {
        "CidrBlock": "10.0.0.0/16",
        "DhcpOptionsId": "dopt-00dae19f3bf38dbd4",
        "State": "pending",
        "VpcId": "vpc-06f6bc7820c899054",
        "OwnerId": "778377806623",
        "InstanceTenancy": "default",
        "Ipv6CidrBlockAssociationSet": [],
        "CidrBlockAssociationSet": [
            {
                "AssociationId": "vpc-cidr-assoc-010c8938bd32e3d1a",
                "CidrBlock": "10.0.0.0/16",
                "CidrBlockState": {
                    "State": "associated"
                }
            }
        ],
        "IsDefault": false
    }
}

aws ec2 create-subnet --vpc-id vpc-05ae1d8e75483e8a2 --cidr-block 192.0.1.0/24

{
    "Subnet": {
        "AvailabilityZone": "eu-north-1c",
        "AvailabilityZoneId": "eun1-az3",
        "AvailableIpAddressCount": 251,
        "CidrBlock": "192.0.1.0/24",
        "DefaultForAz": false,
        "MapPublicIpOnLaunch": false,
        "State": "available",
        "SubnetId": "subnet-023c4c69dfc7dde6f",
        "VpcId": "vpc-05ae1d8e75483e8a2",
        "OwnerId": "778377806623",
        "AssignIpv6AddressOnCreation": false,
        "Ipv6CidrBlockAssociationSet": [],
        "SubnetArn": "arn:aws:ec2:eu-north-1:778377806623:subnet/subnet-023c4c69dfc7dde6f",
        "EnableDns64": false,
        "Ipv6Native": false,
        "PrivateDnsNameOptionsOnLaunch": {
            "HostnameType": "ip-name",
            "EnableResourceNameDnsARecord": false,
            "EnableResourceNameDnsAAAARecord": false
        }
    }
}

aws ec2 create-subnet --vpc-id vpc-05ae1d8e75483e8a2 --cidr-block 192.0.2.0/24

{
    "Subnet": {
        "AvailabilityZone": "eu-north-1c",
        "AvailabilityZoneId": "eun1-az3",
        "AvailableIpAddressCount": 251,
        "CidrBlock": "192.0.2.0/24",
        "DefaultForAz": false,
        "MapPublicIpOnLaunch": false,
        "State": "available",
        "SubnetId": "subnet-0032b909122bbaaae",
        "VpcId": "vpc-05ae1d8e75483e8a2",
        "OwnerId": "778377806623",
        "AssignIpv6AddressOnCreation": false,
        "Ipv6CidrBlockAssociationSet": [],
        "SubnetArn": "arn:aws:ec2:eu-north-1:778377806623:subnet/subnet-0032b909122bbaaae",
        "EnableDns64": false,
        "Ipv6Native": false,
        "PrivateDnsNameOptionsOnLaunch": {
            "HostnameType": "ip-name",
            "EnableResourceNameDnsARecord": false,
            "EnableResourceNameDnsAAAARecord": false
        }
    }
}

aws ec2 create-internet-gateway

{
    "InternetGateway": {
        "Attachments": [],
        "InternetGatewayId": "igw-0850f8792e0193ea5",
        "OwnerId": "778377806623",
        "Tags": []
    }
}

aws ec2 attach-internet-gateway --internet-gateway-id igw-0850f8792e0193ea5 --vpc-id vpc-05ae1d8e75483e8a2

attached gateway to vpc

aws ec2 create-route-table --vpc-id vpc-05ae1d8e75483e8a2

{
    "RouteTable": {
        "Associations": [],
        "PropagatingVgws": [],
        "RouteTableId": "rtb-057020cc1b1475580",
        "Routes": [
            {
                "DestinationCidrBlock": "192.0.0.0/16",
                "GatewayId": "local",
                "Origin": "CreateRouteTable",
                "State": "active"
            }
        ],
        "Tags": [],
        "VpcId": "vpc-05ae1d8e75483e8a2",
        "OwnerId": "778377806623"
    }
}

aws ec2 associate-route-table --route-table-id rtb-057020cc1b1475580 --subnet-id subnet-023c4c69dfc7dde6f

{
    "AssociationId": "rtbassoc-08c5ffdf3e0d6ebad",
    "AssociationState": {
        "State": "associated"
    }
}

aws ec2 associate-route-table --route-table-id rtb-057020cc1b1475580 --subnet-id subnet-0032b909122bbaaae

{
    "AssociationId": "rtbassoc-0045e5c41efd7b209",
    "AssociationState": {
        "State": "associated"
    }
}

aws ec2 create-route --route-table-id rtb-057020cc1b1475580 --destination-cidr-block 0.0.0.0/0 --gateway-id igw-0850f8792e0193ea5

{
    "Return": true
}

aws ec2 create-security-group --group-name sga192 --description "sga" --vpc-id vpc-05ae1d8e75483e8a2

{
    "GroupId": "sg-04b608a3628688b3a"
}

aws ec2 create-security-group --group-name sgb192 --description "sgb" --vpc-id vpc-05ae1d8e75483e8a2

{
    "GroupId": "sg-02bad8b45ce0bf840"
}

aws ec2 run-instances --image-id ami-0fe8bec493a81c7da --instance-type t3.micro --key-name sshv2 --subnet-id subnet-023c4c69dfc7dde6f --security-group-ids sg-04b608a3628688b3a

{
    "Groups": [],
    "Instances": [
        {
            "AmiLaunchIndex": 0,
            "ImageId": "ami-0fe8bec493a81c7da",
            "InstanceId": "i-05d839612747b3460",
            "InstanceType": "t3.micro",
            "KeyName": "sshv2",
            "LaunchTime": "2023-11-14T16:38:16.000Z",
            "Monitoring": {
                "State": "disabled"
            },
            "Placement": {
                "AvailabilityZone": "eu-north-1c",
                "GroupName": "",
                "Tenancy": "default"
            },
            "PrivateDnsName": "ip-192-0-1-105.eu-north-1.compute.internal",
            "PrivateIpAddress": "192.0.1.105",
            "ProductCodes": [],
            "PublicDnsName": "",
            "State": {
                "Code": 0,
                "Name": "pending"
            },
            "StateTransitionReason": "",
            "SubnetId": "subnet-023c4c69dfc7dde6f",
            "VpcId": "vpc-05ae1d8e75483e8a2",
            "Architecture": "x86_64",
            "BlockDeviceMappings": [],
            "ClientToken": "fbf37b35-9355-4e05-9640-c8ad89007f90",
            "EbsOptimized": false,
            "EnaSupport": true,
            "Hypervisor": "xen",
            "NetworkInterfaces": [
                {
                    "Attachment": {
                        "AttachTime": "2023-11-14T16:38:16.000Z",
                        "AttachmentId": "eni-attach-0e0ff0dd2a1fd3a6a",
                        "DeleteOnTermination": true,
                        "DeviceIndex": 0,
                        "Status": "attaching",
                        "NetworkCardIndex": 0
                    },
                    "Description": "",
                    "Groups": [
                        {
                            "GroupName": "sga192",
                            "GroupId": "sg-04b608a3628688b3a"
                        }
                    ],
                    "Ipv6Addresses": [],
                    "MacAddress": "0e:14:35:8c:69:e8",
                    "NetworkInterfaceId": "eni-0f6bea6ebdc4683ac",
                    "OwnerId": "778377806623",
                    "PrivateIpAddress": "192.0.1.105",
                    "PrivateIpAddresses": [
                        {
                            "Primary": true,
                            "PrivateIpAddress": "192.0.1.105"
                        }
                    ],
                    "SourceDestCheck": true,
                    "Status": "in-use",
                    "SubnetId": "subnet-023c4c69dfc7dde6f",
                    "VpcId": "vpc-05ae1d8e75483e8a2",
                    "InterfaceType": "interface"
                }
            ],
            "RootDeviceName": "/dev/sda1",
            "RootDeviceType": "ebs",
            "SecurityGroups": [
                {
                    "GroupName": "sga192",
                    "GroupId": "sg-04b608a3628688b3a"
                }
            ],
            "SourceDestCheck": true,
            "StateReason": {
                "Code": "pending",
                "Message": "pending"
            },
            "VirtualizationType": "hvm",
            "CpuOptions": {
                "CoreCount": 1,
                "ThreadsPerCore": 2
            },
            "CapacityReservationSpecification": {
                "CapacityReservationPreference": "open"
            },
            "MetadataOptions": {
                "State": "pending",
                "HttpTokens": "optional",
                "HttpPutResponseHopLimit": 1,
                "HttpEndpoint": "enabled",
                "HttpProtocolIpv6": "disabled",
                "InstanceMetadataTags": "disabled"
            },
            "EnclaveOptions": {
                "Enabled": false
            },
            "PrivateDnsNameOptions": {
                "HostnameType": "ip-name",
                "EnableResourceNameDnsARecord": false,
                "EnableResourceNameDnsAAAARecord": false
            }
        }
    ],
    "OwnerId": "778377806623",
    "ReservationId": "r-0aaa425307ce0cfba"
}

aws ec2 run-instances --image-id ami-0fe8bec493a81c7da --instance-type t3.micro --key-name sshv2 --subnet-id subnet-0032b909122bbaaae -
-security-group-ids sg-02bad8b45ce0bf840

{
    "Groups": [],
    "Instances": [
        {
            "AmiLaunchIndex": 0,
            "ImageId": "ami-0fe8bec493a81c7da",
            "InstanceId": "i-002a0904554ee6cb2",
            "InstanceType": "t3.micro",
            "KeyName": "sshv2",
            "LaunchTime": "2023-11-14T16:56:02.000Z",
            "Monitoring": {
                "State": "disabled"
            },
            "Placement": {
                "AvailabilityZone": "eu-north-1c",
                "GroupName": "",
                "Tenancy": "default"
            },
            "PrivateDnsName": "ip-192-0-2-124.eu-north-1.compute.internal",
            "PrivateIpAddress": "192.0.2.124",
            "ProductCodes": [],
            "PublicDnsName": "",
            "State": {
                "Code": 0,
                "Name": "pending"
            },
            "StateTransitionReason": "",
            "SubnetId": "subnet-0032b909122bbaaae",
            "VpcId": "vpc-05ae1d8e75483e8a2",
            "Architecture": "x86_64",
            "BlockDeviceMappings": [],
            "ClientToken": "d3da5dd2-e00d-4b5c-9faf-5b4b7f90bd5d",
            "EbsOptimized": false,
            "EnaSupport": true,
            "Hypervisor": "xen",
            "NetworkInterfaces": [
                {
                    "Attachment": {
                        "AttachTime": "2023-11-14T16:56:02.000Z",
                        "AttachmentId": "eni-attach-0b5fccf689185bec5",
                        "DeleteOnTermination": true,
                        "DeviceIndex": 0,
                        "Status": "attaching",
                        "NetworkCardIndex": 0
                    },
                    "Description": "",
                    "Groups": [
                        {
                            "GroupName": "sgb192",
                            "GroupId": "sg-02bad8b45ce0bf840"
                        }
                    ],
                    "Ipv6Addresses": [],
                    "MacAddress": "0e:3e:f6:14:f3:ea",
                    "NetworkInterfaceId": "eni-0935025421cdad8ba",
                    "OwnerId": "778377806623",
                    "PrivateIpAddress": "192.0.2.124",
                    "PrivateIpAddresses": [
                        {
                            "Primary": true,
                            "PrivateIpAddress": "192.0.2.124"
                        }
                    ],
                    "SourceDestCheck": true,
                    "Status": "in-use",
                    "SubnetId": "subnet-0032b909122bbaaae",
                    "VpcId": "vpc-05ae1d8e75483e8a2",
                    "InterfaceType": "interface"
                }
            ],
            "RootDeviceName": "/dev/sda1",
            "RootDeviceType": "ebs",
            "SecurityGroups": [
                {
                    "GroupName": "sgb192",
                    "GroupId": "sg-02bad8b45ce0bf840"
                }
            ],
            "SourceDestCheck": true,
            "StateReason": {
                "Code": "pending",
                "Message": "pending"
            },
            "VirtualizationType": "hvm",
            "CpuOptions": {
                "CoreCount": 1,
                "ThreadsPerCore": 2
            },
            "CapacityReservationSpecification": {
                "CapacityReservationPreference": "open"
            },
            "MetadataOptions": {
                "State": "pending",
                "HttpTokens": "optional",
                "HttpPutResponseHopLimit": 1,
                "HttpEndpoint": "enabled",
                "HttpProtocolIpv6": "disabled",
                "InstanceMetadataTags": "disabled"
            },
            "EnclaveOptions": {
                "Enabled": false
            },
            "PrivateDnsNameOptions": {
                "HostnameType": "ip-name",
                "EnableResourceNameDnsARecord": false,
                "EnableResourceNameDnsAAAARecord": false
            }
        }
    ],
    "OwnerId": "778377806623",
    "ReservationId": "r-0a4efc79a7a58e048"
}

aws ec2 authorize-security-group-ingress --group-id sg-04b608a3628688b3a --protocol tcp --port 22 --source-security-group sg-02bad8b45ce0bf840
aws ec2 authorize-security-group-ingress --group-id sg-04b608a3628688b3a --protocol tcp --port 80 --source-security-group sg-02bad8b45ce0bf840
aws ec2 authorize-security-group-egress --group-id sg-04b608a3628688b3a --protocol all --cidr 0.0.0.0/0


aws ec2 authorize-security-group-ingress --group-id sg-02bad8b45ce0bf840 --protocol all --source-security-group sg-04b608a3628688b3a
aws ec2 authorize-security-group-egress --group-id sg-02bad8b45ce0bf840--protocol all --cidr 0.0.0.0/0


aws ec2 authorize-security-group-ingress --group-id sg-04b608a3628688b3a --protocol all --cidr 192.0.0.0/16

{
    "Return": true,
    "SecurityGroupRules": [
        {
            "SecurityGroupRuleId": "sgr-02b02a614aea5c9d5",
            "GroupId": "sg-04b608a3628688b3a",
            "GroupOwnerId": "778377806623",
            "IsEgress": false,
            "IpProtocol": "-1",
            "FromPort": -1,
            "ToPort": -1,
            "CidrIpv4": "192.0.0.0/16"
        }
    ]
}

http://16.171.239.103/wp-admin/setup-config.php
