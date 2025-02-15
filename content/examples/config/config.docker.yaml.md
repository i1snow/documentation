```yaml
# See detailed configuration settings : https://www.pomerium.com/docs/reference/


# this is the domain the identity provider will callback after a user authenticates
authenticate_service_url: https://authenticate.localhost.pomerium.io

####################################################################################
# Certificate settings:  https://www.pomerium.com/docs/reference/certificates.html #
# The example below assumes a certificate and key file will be mounted to a volume #
# available to the  Docker image.                                                  #
####################################################################################
certificate_file: /pomerium/cert.pem
certificate_key_file: /pomerium/privkey.pem

##################################################################################
# Identity provider settings : https://www.pomerium.com/docs/identity-providers/ #
# The keys required in this section vary depending on your IdP. See the          #
# appropriate docs for your IdP to configure Pomerium accordingly.               #
##################################################################################
idp_provider: google
idp_client_id: REPLACE_ME
idp_client_secret: REPLACE_ME

# Generate 256 bit random keys  e.g. `head -c32 /dev/urandom | base64`
cookie_secret: V2JBZk0zWGtsL29UcFUvWjVDWWQ2UHExNXJ0b2VhcDI=

# https://pomerium.com/reference/#routes
routes:
  - from: https://verify.localhost.pomerium.io
    to: http://verify:8000
    policy:
      - allow:
          or:
            - email:
                is: user@example.com
    pass_identity_headers: true
```
