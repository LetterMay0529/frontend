<template>
    <div>
        <NavBar />

        <div class="container">
            <div class="row">
                <div class="col-md-4 offset-md-4 mt-3">
                    <b-card header="User Login">
                        <form action="#">
                            <div class="form-group">
                                <label for="name">Name:</label>
                                <input type="email" id="name" class="form-control">
                            </div>
                            <div class="form-group">
                                <label for="email">Email:</label>
                                <input type="email" id="email" class="form-control">
                            </div>
                            <div class="form-group">
                                <label for="password">Password:</label>
                                <input type="password"  id="password" class="form-control">
                            </div>
                            <div class="form-group">
                                <button class="btn btn-primary">Signup</button>
                            </div>
                        </form>
                    </b-card>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
   
}
</script>