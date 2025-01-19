Sumbission to the challenge - https://roadmap.sh/projects/basic-dns
  

### Task #1 - Custom Domain for GitHub Pages

  

  

For this task I have configured www.gh.kzwolenik.com as *Custom domain* in the GitHub Pages setting.

Additionaly I have added a DNS record in the CloudFlare admin panel

|Type|Name|Content|
|--|--|--|
|CNAME|www.gh|kzwolenik95.github.io|

  

I have follower official docs: https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site

  

Now the GitHub Pages can be accessed at https://www.gh.kzwolenik.com/

  
  

### Task #2 - Custom Domain for DigitalOcean Droplet

  

For this task I have copied terraform files from previous challenge https://github.com/kzwolenik95/static-site-server

I have made several updates to the Terraform code:

1.  Added a Cloudflare provisioner to manage DNS resources within Terraform.
2.  Implemented code to dynamically fetch the server IP and create the corresponding DNS record in Cloudflare.
3.  Included a local provisioner in the server's Terraform resource to execute the `deploy.sh` script locally, deploying my website files.

To  make  the  code  functional,  you  need  to  provide  the  following  API  tokens:

  

Cloudflare  API  token:  I've set  it  as  an  environment  variable:


    export  TF_VAR_cloudflare_api_token=<your-cloudflare-token>


DigitalOcean  API  token:  I've set  it  as  an  environment  variable:


    export  DO_PAT=<your-digitalocean-token>

You also need to set variables: 
*apex-domain* and *subdomain*
apex-domain is your domain in CloudFlare, and subdomain is the prefix that will be useed for example blog.example.com, use @ if you want to use the apex domain directly
For these I recommend using terraform.tfvars file

  
Now,  with  just  one  command,  you  can  configure  and  deploy  everything  seamlessly.

    terraform apply -var "do_token=${DO_PAT}" -var "pvt_key=$HOME/.ssh/id_rsa"

