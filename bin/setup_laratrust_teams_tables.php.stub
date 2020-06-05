<?php

use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

class LaratrustSetupTeamsTables extends Migration
{
    /**
     * Run the migrations.
     *
     * @return void
     */
    public function up()
    {
        if (config('laratrust.teams.enabled', false)) {

            // Create table for storing teams
            Schema::create(config('laratrust.tables.teams', 'teams'), function (Blueprint $table) {
                $table->increments('id');
                $table->string('name')->unique();
                $table->string('display_name')->nullable();
                $table->string('description')->nullable();
                $table->timestamps();
            });

            // Modify the role user table
            Schema::table(config('laratrust.tables.role_user', 'role_user'), function (Blueprint $table) {
                $table->unsignedInteger(config('laratrust.foreign_keys.team', 'team_id'))->nullable();

                $table->dropPrimary([
                    config('laratrust.foreign_keys.user', 'user_id'),
                    config('laratrust.foreign_keys.role', 'role_id'),
                    'user_type'
                ]);

                $table->foreign(config('laratrust.foreign_keys.team', 'team_id'))
                    ->references('id')
                    ->on(config('laratrust.tables.teams', 'teams'))
                    ->onUpdate('cascade')
                    ->onDelete('cascade');

                $table->unique([
                    config('laratrust.foreign_keys.user', 'user_id'),
                    config('laratrust.foreign_keys.role', 'role_id'),
                    'user_type',
                    config('laratrust.foreign_keys.team', 'team_id')
                ]);
            });
            
            // Modify the permission user table
            Schema::table(config('laratrust.tables.permission_user', 'permission_user'), function (Blueprint $table) {
                $table->unsignedInteger(config('laratrust.foreign_keys.team', 'team_id'))->nullable();

                $table->dropPrimary([
                    config('laratrust.foreign_keys.user', 'user_id'),
                    config('laratrust.foreign_keys.permission', 'permission_id'),
                    'user_type'
                ]);

                $table->foreign(config('laratrust.foreign_keys.team', 'team_id'))
                    ->references('id')
                    ->on(config('laratrust.tables.teams', 'teams'))
                    ->onUpdate('cascade')
                    ->onDelete('cascade');

                $table->unique([
                    config('laratrust.foreign_keys.user', 'user_id'),
                    config('laratrust.foreign_keys.permission', 'permission_id'),
                    'user_type',
                    config('laratrust.foreign_keys.team', 'team_id')
                ]);
            });
        }
    }

    /**
     * Reverse the migrations.
     *
     * @return void
     */
    public function down()
    {
        //
    }
}
