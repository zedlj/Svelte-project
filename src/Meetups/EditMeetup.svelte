<script>
    import { createEventDispatcher } from 'svelte';
    import { isEmpty, isValidEmail } from '../helpers/validation'; 
    import TextInput from '../UI/TextInput.svelte';
    import Button from '../UI/Button.svelte';
    import Modal from '../UI/Modal.svelte';

    let title = '';
    let subtitle = '';
    let address = '';
    let email = '';
    let description = '';
    let imageUrl = '';
    let formIsValid = false;

    const dispatch = createEventDispatcher();

    // Don't need to initialise reactive variabkes above, Svelte does this on initialisation
    $: titleValid = !isEmpty(title);
    $: subtitleValid = !isEmpty(subtitle);
    $: addressValid = !isEmpty(address);
    $: descriptionValid = !isEmpty(description);
    $: imageUrlValid = !isEmpty(imageUrl);
    $: emailValid = isValidEmail(email);
    $: console.log('email valid', emailValid);
    $: formIsValid = titleValid && subtitleValid && addressValid && descriptionValid && imageUrlValid && emailValid;

    function submitForm() {
        dispatch('save', {
            title: title,
            subtitle: subtitle,
            address: address,
            email: email,
            description: description,
            imageUrl: imageUrl,
        });
    }

    function cancel() {
        dispatch('cancel');
    }

</script>
<Modal title="Meetup details" on:cancel>
    <form on:submit|preventDefault="{submitForm}">
        <TextInput 
            id={"title"}
            label={"Title"}
            value={title}
            on:input={event => (title = event.target.value)}
            type="text"
            valid={titleValid}
            validityMessage="This field is required"
        />
        <TextInput 
            id={"subtitle"}
            label={"Subtitle"}
            value={subtitle}
            on:input={event => (subtitle = event.target.value)}
            type="text"
            valid={subtitleValid}
            validityMessage="This field is required"
        />
        <TextInput 
            id={"imageurl"}
            label={"Image URL"}
            value={imageUrl}
            on:input={event => (imageUrl = event.target.value)}
            type="text"
            valid={imageUrlValid}
            validityMessage="This field is required"
        />
        <TextInput 
            id={"email"}
            label={"Email"}
            value={email}
            on:input={event => (email = event.target.value)}
            type="text"
            valid={emailValid}
            validityMessage="This field is required- please enter a valid email"
        />
        <TextInput 
            id={"address"}
            label={"Address"}
            value={address}
            on:input={event => (address = event.target.value)}
            type="text"
            valid={addressValid}
            validityMessage="This field is required"
        />
        <TextInput 
            id={"description"}
            label={"Description"}
            value={description}
            on:input={event => (description = event.target.value)}
            controlType="textarea"
            valid={descriptionValid}
            validityMessage="This field is required"
        />
    </form>
    <div slot="footer">
        <Button type="button" mode="outline" on:click={cancel}>Cancel</Button>
        <Button type="button" on:click={submitForm} disabled={!formIsValid}>Save</Button>
    </div>
</Modal>

<style>
    form {
        width: 100%;
        max-width: 90%;
        margin: auto;
    }
</style>