<script>
    import Header from './UI/Header.svelte';
    import MeetupGrid from './Meetups/MeetupGrid.svelte';
    import TextInput from './UI/TextInput.svelte';
    import Button from './UI/Button.svelte';

    let title = '';
    let subtitle = '';
    let address = '';
    let email = '';
    let description = '';
    let imageUrl = '';

    let meetups = [
        {
            id: 'm1',
            title: 'Coding Bootcamp',
            subtitle: 'learn the basics of web development',
            description: 'JS, HTML, CSS',
            imageUrl: 'https://images.unsplash.com/photo-1516259762381-22954d7d3ad2?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxzZWFyY2h8Mnx8Y29kZXxlbnwwfHwwfHw%3D&auto=format&fit=crop&w=2000&q=60',
            address: '27th Nerd rd',
            contactEmail: 'coder@code.com',
        },
        {
            id: 'm2',
            title: 'Swim school',
            subtitle: 'learn the basics of swimming',
            description: 'front and back stroke',
            imageUrl: 'https://images.unsplash.com/photo-1530549387789-4c1017266635?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1770&q=80',
            address: 'Pool lane',
            contactEmail: 'swimmer@swim.com',
        }
    ];

    function addMeetup() {
        const newMeetup = {
            id: Math.random.toString(),
            title: title,
            subtitle: subtitle,
            description: description,
            imageUrl: imageUrl,
            contactEmail: email,
            address: address,
        }

        meetups = [newMeetup, ...meetups];
    }


</script>

<style>
    form {
        width: 30rem;
        max-width: 90%;
        margin: auto;
    }
</style>


<Header />

<main style="margin-top: 70px;" >
    <form on:submit|preventDefault="{addMeetup}">
        <TextInput 
            id={"title"}
            label={"Title"}
            value={title}
            on:input={event => (title = event.target.value)}
            type="text"
        />
        <TextInput 
            id={"subtitle"}
            label={"Subtitle"}
            value={subtitle}
            on:input={event => (subtitle = event.target.value)}
            type="text"
        />
        <TextInput 
            id={"imageurl"}
            label={"Image URL"}
            value={imageUrl}
            on:input={event => (imageUrl = event.target.value)}
            type="text"
        />
        <TextInput 
            id={"email"}
            label={"Email"}
            value={email}
            on:input={event => (email = event.target.value)}
            type="text"
        />
        <TextInput 
            id={"address"}
            label={"Address"}
            value={address}
            on:input={event => (address = event.target.value)}
            type="text"
        />
        <TextInput 
            id={"description"}
            label={"Description"}
            value={description}
            on:input={event => (description = event.target.value)}
            controlType="textarea"
        />
        <Button type="submit" caption="Save" />
    </form>

    <MeetupGrid {meetups}/>

</main>



