## Using Cloudflare Managed Domains With Vercel: Error: Too many redirects

## Scenario

Your frontend is finally complete, congratulations! Now you just need to deploy to vercel and add your cloudflare managed domain.

You go over to [vercel](https://vercel.com) and create a deployment from a github repository, probably. And it deploys just fine. Now it's time to add the secret sauce, your custom domain.


![adding-custom-domain.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1661105927092/NEQMfsysL.png align="left")


![choosing-default.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1661105950956/DUf2fVP0Z.png align="left")

You choose the default settings and head over to cloudflare dashboard to change the DNS settings to point to vercel's servers. You've done these DNS setttings before, nothing can go wrong, right? Well DNS is a world of mystery and terror (mostly).


![cloudflare-dash-dns.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1661106324915/DLBpRimPG.png align="left")

## LGTM! SHIP IT

![too-many-redirects.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1661106675507/xkxgSlJ_r.png align="left")

Oops, the ship has sunk.

Stop before you clear cookies, reinstall your browser or worse.

### Why Does This Happen

This is due to SSL/TLS being set to "Flexible" in the cloudlare dashboard for your domain.
When SSL/TLS is set to flexible cloudflare servers may send HTTP to Vercel's servers. Vercel's servers do not like HTTP when there is a certificate present for your domain, which is automatically assigned by Vercel after you change the DNS settings.

Vercel also has a [guide](https://vercel.com/guides/resolve-err-too-many-redirects-when-using-cloudflare-proxy-with-vercel) about this, you can check that out as well.

## The Fix

To fix this, find the SSL/TLS settings in the cloudflare dashboard.


![ssl-tls-settings.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1661107137068/OdlRyhNpt.png align="left")


![ssl-tls-set-to-flexible.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1661107156459/tKm80AFYt.png align="left")

Yep, it's set to flexible. Let's change that.


![correct-settings.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1661107181993/L-m-Pbcfo.png align="left")

And we are done! It should start working in a minute at most.

![it-works.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1661107522090/0laZ5G28X.png align="left")


![connected-to-edge.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1661107937839/sOyXAxPC2.png align="left")

As you can see, we are living on the edge.



Thanks for reading. Let me know in the comments if you have any questions or suggestions!
