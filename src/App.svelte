<script>
    import Header from './UI/Header.svelte';
    import MeetupGrid from './Meetups/MeetupGrid.svelte';
    import EditMeetup from './Meetups/EditMeetup.svelte';
    import Button from './UI/Button.svelte';

    let editMode;

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

    function addMeetup(event) {
        const newMeetup = {
            id: Math.random.toString(),
            title: event.detail.title,
            subtitle: event.detail.subtitle,
            description: event.detail.description,
            imageUrl: event.detail.imageUrl,
            contactEmail: event.detail.email,
            address: event.detail.address,
        }

        meetups = [newMeetup, ...meetups];
        editMode = null;
    }

    function toggleFavourite(event){
        console.log("fave toggled", event)
        const id = event.detail;
        // Returns a meetup object where true (searching via id)
        // Spread operator so original is not mutated
        const updatedMeetup = { ...meetups.find(element => element.id === id) };
        updatedMeetup.isFavourite = !updatedMeetup.isFavourite;
        const meetupIndex = meetups.findIndex(element => element.id === id);
        const updatedMeetups = [...meetups];
        updatedMeetups[meetupIndex] = updatedMeetup;
        meetups = updatedMeetups;
        console.log(updatedMeetups)
    }

    function cancelEdit() {
        editMode = null;
    }


</script>

<style>

    .meetup-controls {
        margin: 1rem;
    }

</style>


<Header />

<main style="margin-top: 70px;" >
    <div class="meetup-controls">
        <Button on:click="{() => editMode = 'add'}">New Meetup</Button>   
    </div> 
    {#if editMode === 'add'}
        <EditMeetup on:save="{addMeetup}" on:cancel={cancelEdit}/>
    {/if}  
    <MeetupGrid {meetups} on:togglefavourite="{toggleFavourite}"/>
</main>



