**The format of the email**：a-b\_.@x-x.com

**The limit of the login password**：length: 9~16，numbers, characters, and symbols.

**The limit of the fund password**：length 6~16，numbers, characters, and symbols.

---

**Register**：Email

**Login**： email + password.

```
          If the user has configured phone or GA or both, then the user can choose one of them to verify.
```

**Bind Phone**: will verify the email code.

**Change Password**:

```
       no phone or GA configured: verify the captcha.

       phone or GA configured: choose one of them to verify.
```

**Reset Password**:

```
       no phone or GA configured: email + captcha

       only phone configured: email + captcha + phone

       phone & GA configured: email + captcha + phone/GA
```

**Set Fund Password**:

```
       no GA configured: phone

       GA configured: phone + GA
```

**Change Fund Password**:

```
       no GA configured: old-pass + phone

       GA configured: old-pass + phone + GA
```

**Reset Fund Password**:

```
       no GA configured: email + phone

       GA configured: email + phone + GA
```

**Fund Password Expire time**: can be set by the user, to: everytime, every hour, and everyday.

**Viewing the Withdrawal Page**: phone, GA, fund pass all set + KYC verified

**Add Withdraw Address**: phone + GA + fund pass

**Withdrawal**: Email + Phone + Ga + fund pass

