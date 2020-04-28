
* TOC
{:toc}

## Styled error Messages on elementor forms

Just paste the code to your theme `functions.php` or put the `script` tags content on a seperate JS file.
**Preview**: [https://prnt.sc/s7mklz](https://prnt.sc/s7mklz).

```
add_action( 'wp_footer', function () {
   ?>
    <script>
        let forms = document.querySelectorAll( '.elementor-form' );

        forms.forEach(function (form) {

            let inputs = form.querySelectorAll('.elementor-field');
            let submit = form.querySelector('button[type="submit"]');

            inputs.forEach(function(input) {
                input.addEventListener('invalid', function(e) {
                    e.preventDefault();

                    let errorEl = document.createElement('div');
                    errorEl.classList.add('error');
                    errorEl.style.color = 'red';
                    errorEl.innerHTML = this.validationMessage;

                    this.parentElement.parentNode.insertBefore(errorEl, this.parentElement.nextSibling);
                });
            });

            submit.addEventListener('click', function (e) {
                removeErrors(form);
            });

            function removeErrors(form) {
                form.querySelectorAll('.error').forEach(function (error) {
                    error.remove();
                });
            }
        });

    </script>
    <?php
});
```

### Support
If you have any issues with the code I post here, feel free to contact me at [https://postmansmtp.com](https://postmansmtp.com)

**Still not familiar with Post SMTP?** 
Post SMTP is the most powerfull SMTP plugin for WordPress **with more then 100,000 active installs**. 
check it here: [https://wordpress.org/plugins/post-smtp/](https://wordpress.org/plugins/post-smtp/)
