
'''
#include "core.h"

void handle_warrior(t_obj *unit)
{
    t_obj *enemy;

    // найти ближайшего врага
    enemy = core_get_nearest_enemy(unit);

    if (enemy)
    {
        // если враг есть — атакуем
        core_action_attack(unit, enemy);
    }
    else
    {
        // если врагов не видно — двигаться к ближайшему
        t_pos pos = core_get_nearest_enemy_pos(unit);
        core_action_moveTowards(unit, pos);
    }
}

void bot_tick()
{
    static int tick = 0;
    t_obj **units;
    int count;

    tick++;

    // спавн воина
    if (core_get_gems() > 150 && tick >= 175)
    {
        core_action_createUnit(UNIT_WARRIOR);
    }

    // получить всех своих юнитов
    units = core_get_objs_filter(ft_is_own_team_unit);
    count = core_get_objs_filter_count(ft_is_own_team_unit);

    // логика для каждого юнита
    for (int i = 0; i < count; i++)
    {
        handle_warrior(units[i]);
    }
}
'''



https://coregame.sh/wiki/v0.0.4/reference/config/core_get_unitConfig

```


#include "core.h"

void handle_unit(t_obj *unit)
{
    t_obj *enemy;
    t_pos gem;

    enemy = core_get_nearest_enemy(unit);

    if (enemy)
    {
        core_action_attack(unit, enemy);
        return;
    }

    gem = core_get_nearest_gem(unit);
    core_action_moveTowards(unit, gem);
}

void bot_tick()
{
    t_obj **units;
    int count;
    int i;

    units = core_get_objs_filter(ft_is_own_team_unit);
    count = core_get_objs_filter_count(ft_is_own_team_unit);

    i = 0;
    while (i < count)
    {
        handle_unit(units[i]);
        i++;
    }

    if (core_get_gems() >= 10)
        core_action_createUnit(UNIT_WARRIOR);
}




```
```
void handle_unit(t_obj *unit)
{
    t_obj *enemy;
    t_pos gem;

    enemy = core_get_nearest_enemy(unit);

    if (enemy)
    {
        core_action_attack(unit, enemy);
        return;
    }

    gem = core_get_nearest_gem(unit);
    core_action_moveTowards(unit, gem);
}

void bot_tick()
{
    t_obj **units;
    int count;
    int i;

    units = core_get_objs_filter(ft_is_own_team_unit);
    count = core_get_objs_filter_count(ft_is_own_team_unit);

    i = 0;
    while (i < count)
    {
        handle_unit(units[i]);
        i++;
    }

    if (core_get_gems() >= 5)
        core_action_createUnit(UNIT_WARRIOR);
}
```




